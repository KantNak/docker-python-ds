FROM python:3.9

ENV PYTHONUNBUFFERED 1

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    fish \
    git

COPY user-settings /root/.jupyter/lab/user-settings

ADD requirements.txt .
RUN pip install --upgrade pip && \
    pip install --no-cache-dir  -r requirements.txt
RUN pip install --no-cache-dir \
    torch \
    torchvision \
    torchaudio \
    --extra-index-url https://download.pytorch.org/whl/cpu

# for fish
SHELL [ "/usr/bin/fish", "-c" ]
RUN curl https://git.io/fisher --create-dirs -sLo ~/.config/fish/functions/fisher.fish
RUN fisher install oh-my-fish/theme-coffeeandcode

RUN echo 'alias jupyter-lab="jupyter lab --ip=0.0.0.0 --allow-root --no-browser --port=8888"' >> ~/.config/fish/config.fish
RUN echo 'alias cookiecutter-ds="cookiecutter https://github.com/drivendata/cookiecutter-data-science"' >> ~/.config/fish/config.fish