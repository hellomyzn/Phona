# Phona – English Pronunciation Visualizer

Phona is a tool that helps learners see and understand their English pronunciation.
By recording a short utterance, the service analyzes your speech, converts it into IPA, and highlights which sounds match the target pronunciation and which need improvement.

Why the name “Phona”?

The name comes from the root “phon-”, meaning sound or voice, found in words like phonetics and phoneme.
The simple “-a” ending keeps it friendly and approachable—just like the goal of the project:
making accurate pronunciation accessible, visual, and easy to learn.
This is a my own broiler template for python.

### docker commands
```bash
# run as production (docker-compose up -d --build)
$ make up
# run as develop (docker-compose -f docker-compose-dev.yml up -d --build)
$ make dev
# get into a container (docker-compose exec python bash)
$ make python
# down (docker-compose down)
$ make down
# destroy (docker-compose down --rmi all --volumes --remove-orphans)
$ make destroy
```

### start
1. run container
```bash
$ make up
```
2. reopen in container in vscode
![start_vscode](./docs/images/start_vscode.png)

3. set up [WakaTime](https://wakatime.com/) API key ([link](https://wakatime.com/settings/api-key))
![wakatime_api_key](./docs/images/wakatime_api_key.png)

4. copy `src/common/config/config.template.ini` to `src/common/config/config.ini`
```bash
cp src/common/config/config.template.ini src/common/config/config.ini
cp src/common/config/config.template.ini src/common/config/config.dev.ini
```

### containers
- python
  - python container to exec
- vscode
  - for dev containers in vscode
- plantuml
  - for sequences


### vscode settings
How do I press and hold a key and have it repeat in VSCode?
```bash
$ defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false
```
