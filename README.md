# Weather-Station-Dashboard


title: Weather Station Dashboard
views:
  - title: Weather Overview
    path: weather_overview
    icon: mdi:weather-cloudy
    type: sections
    sections:
      - type: grid
        columns: 3
        cards:
          - type: heading
            icon: ''
            heading: Status Overview
            heading_style: subtitle
          - type: custom:mushroom-template-card
            primary: '{{ states(''sensor.gw2000b_outdoor_temperature'') }}°C'
            secondary: Feels like {{ states('sensor.gw2000b_feels_like_temperature') }}°C
            icon: mdi:thermometer
            layout: vertical
            fill_container: true
            tap_action:
              action: more-info
              entity: sensor.gw2000b_outdoor_temperature
            icon_color: >-
              {% set temp = states('sensor.gw2000b_outdoor_temperature') | float
              %} {% if temp > 25 %}red {% elif temp > 20 %}orange {% elif temp >
              15 %}yellow {% elif temp > 10 %}green {% else %}blue{% endif %}
          - type: custom:mushroom-template-card
            primary: '{{ states(''sensor.gw2000b_humidity'') }}%'
            secondary: Dewpoint {{ states('sensor.gw2000b_dewpoint') }}°C
            icon: mdi:water-percent
            layout: vertical
            fill_container: true
            tap_action:
              action: more-info
              entity: sensor.gw2000b_humidity
            icon_color: >-
              {% set humidity = states('sensor.gw2000b_humidity') | float %} {%
              if humidity > 85 %}red {% elif humidity > 70 %}orange {% elif
              humidity > 60 %}yellow {% else %}green{% endif %}
          - type: custom:mushroom-template-card
            primary: '{{ states(''sensor.rainfall_intensity'') }}'
            secondary: |
              Current Rainfall Intensity Classification
            icon: mdi:weather-rainy
            layout: vertical
            fill_container: true
            tap_action:
              action: more-info
            icon_color: >-
              {% set intensity = states('sensor.rainfall_intensity') %} {% if
              intensity == 'No Rain' %} green  {% elif intensity == 'Light Rain'
              %} blue  {% elif intensity == 'Moderate Rain' %} orange  {% else
              %} red {% endif %}
          - type: custom:mushroom-template-card
            primary: '{{ states(''sensor.gw2000b_rain_rate_piezo'') }} mm/hr'
            secondary: |
              {% if states('sensor.gw2000b_rain_rate_piezo') | float > 0 %}
                Rain Detected!
              {% else %}
                No Rain
              {% endif %}
