# CS2610-Snort-IDS on Dockers

<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#objectives">Objectives</a></li>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li><a href="#setup">Setup</a></li>
    <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>

## About The Project
This project guides you through setting up Snort, a popular Intrusion Detection System, using Docker containers to monitor network traffic and receive alerts for potential intrusions. It includes steps for using a pre-built Docker image by Cisco for Snort 3 and customizing it with your own rules. Let's get started!

### Objectives
- Learn how to set up Snort using Docker containers.
- Understand how to customize Snort with your own rules.
- Learn how to read alerts and identify the rules that triggered them.
- Learn how to disable rules and suppress alerts.
  
### Built With
- Deployment - [Docker Engine](https://www.docker.com/)
- Snort IDS - 

## Setup

### Prerequisites

- Install [Docker Engine](https://docs.docker.com/engine/) with docker-compose

Test installation by running these commands:
```sh
$ docker --help
$ docker compose --help
```

### Step 1: Using Docker for Snort
Start by creating a docker-compose file to set up Snort using Docker containers. You can use the provided configuration in docker-compose.yml:
```yml
version: '3.8'

services:
  snort3:
    image: ciscotalos/snort3
    container_name: snort3
    hostname: snort3
    user: root
    network_mode: host
    cap_add:
      - NET_ADMIN
      - NET_RAW
      - SYS_RAWIO
    working_dir: /home/snorty
    volumes:
      - ./new.rules:/home/snorty/snort3/etc/rules/new.rules:ro
      - ./snort.lua:/home/snorty/snort3/etc/snort/snort.lua:ro
      - ./.bashrc:/root/.bashrc:ro
    command: ["/bin/bash"]
    stdin_open: true
    tty: true
    restart: on-failure:5

```

Run the docker-compose file by using:

```sh
docker compose up -d
```

## Usage

__*Notice that you must first aquire your own Last.FM API key before continuing...__

- Aquire [Last.FM API Key](https://www.last.fm/api) by making an account, it is completely free

- Copy your API Key int the following varible found in actions/actions.py [API_KEY = 'enter your Last.FM API'](https://github.com/cosettekay/Music-Recommendation-Bot/blob/2d3ba8d541ed20286fb06cb84bde47b9c62045ec/actions/actions.py#L16)

Once that is complete, you're read to build your bot

The following code only has to be ran once:
```sh
$ docker build -t my_action_image
```

Running the bot can simiply be ran by using Docker Compose command:
```sh
$ docker compose run rasa
```
Now you can chat with Aca Pella

## Contact

Cosette Tabucol:
- Email - cmtabucol@cpp.edu
- LinkedIn - https://www.linkedin.com/in/cosette-tabucol-a914751b7/

## Acknowledgements

- [Last.FM API](https://www.last.fm/api)
- [Music & Me](https://github.com/Srishti20022/Music-me-Chatbot_song_recommendor_system-)
- [Rasa Assistant on Docker](https://rasa.com/docs/rasa/docker/building-in-docker/)
- [SpaCy Pre-Trained Model](https://spacy.io/models/en)
- [Rasa Data Templates](https://github.com/cedextech/rasa-chatbot-templates/tree/master)
- [Rasa Mood Training Data](https://github.com/RasaHQ/NLU-training-data/tree/main/mood)
- [Getting Music Data with the Last.fm API using Python](https://www.dataquest.io/blog/last-fm-api-python/)

