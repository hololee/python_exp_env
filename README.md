# python AI 개발환경 세팅

## 환경 조건

- Mac os: zsh
- Linux: bash

## [pyenv](https://github.com/pyenv/pyenv)

<details>
<summary><b>설정</b></summary>

1. 설치
   - mac os
        ```shell
        # 설치
        brew update
        brew install pyenv

        # 쉘 환경 설정
        echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
        echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
        echo 'eval "$(pyenv init -)"' >> ~/.zshrc
        ```
   - linux
        ```shell
        # 설치
        apt-get update && apt install build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev curl git libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
        curl https://pyenv.run | bash

        # 쉘 설정.
        echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
        echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
        echo 'eval "$(pyenv init -)"' >> ~/.bashrc
        ```
2. 쉘 리로드
3. python 버전 설정
    ```
    pyenv install 3.12
    ```
</details>

## [direnv](https://github.com/direnv/direnv/wiki/Python#poetry)

<details>
<summary><b>설정</b></summary>

1. 설치
   - mac os
        ```
        brew install direnv
        echo 'eval "$(direnv hook zsh)"' >> ~/.zshrc
       ```
   - linux
        ```
        apt-get install direnv
        echo 'eval "$(direnv hook bash)"' >> ~/.bashrc
        ```
2. `${XDG_CONFIG_HOME:-${HOME}/.config}/direnv/direnvrc`에 아래의 내용을 입력.
    ```
    layout_poetry() {
        poetry env use $(pyenv which python)
        VIRTUAL_ENV=$(poetry env info --path 2>/dev/null ; true)
        poetry install

        PATH_add "$VIRTUAL_ENV/bin"
        export POETRY_ACTIVE=1
        export VIRTUAL_ENV
    }
    ```
3. 쉘 리로드

</details>

## [poetry](https://python-poetry.org/docs/#installation)

<details>
<summary><b>설정</b></summary>

1. 설치
   - mac os
     - pipx 설치
        ```
        brew install pipx
        pipx ensurepath
        ```
     - 쉘 리로드
     - poetry 설치
        ```
        pipx install poetry
        mkdir $ZSH_CUSTOM/plugins/poetry
        poetry completions zsh > $ZSH_CUSTOM/plugins/poetry/_poetry
        ```
     - `~/.zshrc`에 플러그인 추가
        ```
            plugins(
        poetry
        ...
        )
        ```

   - linux
     - pipx 설치
        ```
        apt install pipx
        pipx ensurepath
        ```
     - 쉘 리로드
     - poetry 설치
        ```
        pipx install poetry
        poetry completions bash >> ~/.bash_completion
        ```
</details>
