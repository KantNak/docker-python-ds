FROM python:3.9

ENV PYTHONUNBUFFERED 1

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fish \
    git \
    gcc \
    libgl1-mesa-dev

# Install node with latest version
RUN curl -sL https://deb.nodesource.com/setup_14.x  | bash -
RUN apt-get install -y --no-install-recommends nodejs

COPY user-settings /root/.jupyter/lab/user-settings

ADD requirements.txt .
RUN pip install --upgrade pip && \
    pip install --no-cache-dir --default-timeout=1000  -r requirements.txt
RUN pip install --no-cache-dir --default-timeout=1000 \
    torch==1.9.0+cu111 \
    torchvision==0.10.0+cu111 \
    -f https://download.pytorch.org/whl/torch_stable.html

RUN jupyter serverextension enable --py jupyterlab_code_formatter
RUN jupyter labextension install @ryantam626/jupyterlab_code_formatter

# for fish
SHELL [ "/usr/bin/fish", "-c" ]
RUN curl https://git.io/fisher --create-dirs -sLo ~/.config/fish/functions/fisher.fish
RUN fisher install oh-my-fish/theme-coffeeandcode

RUN echo 'alias jupyter-lab="jupyter lab --ip=0.0.0.0 --allow-root --no-browser --port=8888"' >> ~/.config/fish/config.fish
RUN echo 'alias cookiecutter-ds="cookiecutter https://github.com/drivendata/cookiecutter-data-science"' >> ~/.config/fish/config.fish