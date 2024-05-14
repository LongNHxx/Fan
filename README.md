# Tạo fan bằng công tắc 4 kênh

- sau khi mua công tắc về add home assistant rồi đặt đường dẫn cho các kênh tương ứng với các số như sau
  
  + kênh 1 - số 1: switch.hk_q1_so1
  + kênh 2 - số 2: switch.hk_q1_so2
  + kênh 3 - số 3: switch.hk_q1_so1
  + kênh 4 - đảo gió: switch.hk_q1_dao

#thêm đoạn code này vào configuration.yaml
fan:
  - platform: template
    fans:
      hk_fan:
        friendly_name: "Quạt HK"
        value_template: >
          {{ is_state('switch.hk_q1_so1', 'on') or is_state('switch.hk_q1_so2', 'on') or is_state('switch.hk_q1_so3', 'on') or is_state('switch.hk_q1_dao', 'on') }}
        percentage_template: >
          {% if is_state('switch.hk_q1_so3', 'on') %}
            100
          {% elif is_state('switch.hk_q1_so2', 'on') %}
            67
          {% elif is_state('switch.hk_q1_so1', 'on') %}
            33
          {% else %}
            0
          {% endif %}
        speed_count: 3
        turn_on:
          service: switch.turn_on
          target:
            entity_id: switch.hk_q1_so1
        turn_off:
          - service: switch.turn_off
            target:
              entity_id: 
                - switch.hk_q1_so1
                - switch.hk_q1_so2
                - switch.hk_q1_so3
          - service: switch.turn_off
            target:
              entity_id: switch.hk_q1_dao
        set_percentage:
          - service: switch.turn_off
            target:
              entity_id: 
                - switch.hk_q1_so1
                - switch.hk_q1_so2
                - switch.hk_q1_so3
          - service: switch.turn_on
            data_template:
              entity_id: >
                {% if percentage == 0 %}
                  switch.turn_off
                {% elif percentage > 66 %}
                  switch.hk_q1_so3
                {% elif percentage > 33 %}
                  switch.hk_q1_so2
                {% else %}
                  switch.hk_q1_so1
                {% endif %}
          - service: switch.turn_off
            data_template:
              entity_id: >
                {% if percentage == 0 %}
                  switch.hk_q1_dao
                {% elif percentage > 66 %}
                  switch.hk_q1_so1, switch.hk_q1_so2
                {% elif percentage > 33 %}
                  switch.hk_q1_so1, switch.hk_q1_so3
                {% elif percentage > 0 %}
                  switch.hk_q1_so2, switch.hk_q1_so3
                {% endif %}
        oscillating_template: "{{ is_state('switch.hk_q1_dao', 'on') }}"
        set_oscillating:
          service_template: >
            {% if oscillating %}
              switch.turn_on
            {% else %}
              switch.turn_off
            {% endif %}
          target:
            entity_id: switch.hk_q1_dao

# tạo automation rồi chỉnh sửa bằng yaml thêm code sau:

alias: Sync quạt
description: |+

trigger:
  - platform: state
    entity_id:
      - switch.hk_q1_so1
      - switch.hk_q1_so2
      - switch.hk_q1_so3
condition: []
action:
  - service: switch.turn_off
    data_template:
      entity_id: |
        {% if trigger.to_state.state == 'on' %}
                 {% if trigger.entity_id == 'switch.hk_q1_so1' %}
                   switch.hk_q1_so2, switch.hk_q1_so3
                 {% elif trigger.entity_id == 'switch.hk_q1_so2' %}
                   switch.hk_q1_so1, switch.hk_q1_so3
                 {% else %}
                   switch.hk_q1_so1, switch.hk_q1_so2
                 {% endif %}
               {% endif %}
mode: single


ok, xong vào khởi động lại homeassistant rồi vào thiết bị -> thực thể tìm fan.hk_fan
