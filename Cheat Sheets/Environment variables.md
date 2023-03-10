# Environment variables
#env #environment_variables 

[Видео от Диджитализируй - Как хранить пароли и ключи в коде проектов? Всё о переменных окружения. Пример с Django](https://youtu.be/Y9MRCxq4DIc)

## Linux
#linux #env #environment_variables 

- Get list of environment variables:
```shell
set
```
or with a command:
```sh
env
```

- Access a variable from the shell:
```shell
echo $VAR
```

### OS system-wide

Add variables to the following file `/etc/environment`:
 ```shell
sudo echo "VAR=AAA123" >> /etc/environment
source /etc/environment
```

Or, using text editor:
```shell
sudo vi /etc/environment
```

Example of the line to be added to the file:
```
VAR="AAA123"
```

### User-wide

Add variables to the shell configuration file:
- bash:
```shell
echo "export VAR='AAA123'" >> ~/.bashrc
source ~/.bashrc
```
- zsh:
```shell
echo "export VAR='AAA123'" >> ~/.zshrc
source ~/.zshrc
```

### Session-wide

It makes sense to store a file (e.g. `setenv.sh`) with required environment variables inside a project folder.
```sh
export VAR1='1'
export VAR2='2'
export VAR3='3'
```

Then run that script:
```shell
source ./setenv.sh
```

Or explicitly create variables as follows:
```shell
export VAR="AAA123"
```

Adding folder to the system `$PATH`:
```shell
export PATH="$HOME/bin:$PATH"
```

### Application-wide

#### Python
#python #env #environment_variables 
Let's say we want to pass `VAR='AAA123'` to a python script, which gets variable value with `VAR = os.getenv('VAR')`
```shell
VAR='AAA123' python main.py
```

Several variables can be passed to the script like this:
```shell
VAR1='1' VAR2='2' python main.py
```

#### [[Docker]]
#docker #env #environment_variables 

Start container, passing some environment variables to it.
1. Environment variables exist in the host system (`$OPENAI_API_KEY` and `$OPENAI_CHATGPT_TELEBOT_TOKEN`)
```shell
docker run -e OPENAI_API_KEY --env OPENAI_CHATGPT_TELEBOT_TOKEN -it chatgpt_bot_temp '/bin/sh' 
```
2. Set environment variables explicitly:
```sh
docker run -e VAR1='AAA123' --env VAR2='BBB123' -it chatgpt_bot_temp '/bin/sh'
```
4. Store environments in a file which is to be passed as an argument. File content (`env.txt`):
```text
VARIABLE1=foobar1
VARIABLE2=foobar2
VARIABLE3=foobar3
```
Run docker with the `--env-file` key word:
```sh
docker run --env-file env.txt alpine:3 env
```

### systemd