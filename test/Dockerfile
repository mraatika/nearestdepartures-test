FROM debian:latest

ENV CHROMEDRIVER_VERSION 2.33
ENV GECKODRIVER_VERSION 0.19.0
ENV FIREFOXBROWSER_VERSION 57.0b13

RUN apt-get update
RUN apt-get install -y wget curl gnupg unzip python python-pip

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list \
  && apt-get update \
  && apt-get -y install google-chrome-stable

RUN wget https://ftp.mozilla.org/pub/firefox/releases/$FIREFOXBROWSER_VERSION/linux-x86_64/en-US/firefox-$FIREFOXBROWSER_VERSION.tar.bz2 \
   && tar -xjf "firefox-$FIREFOXBROWSER_VERSION.tar.bz2" \
   && mv firefox /opt/firefox \
   && ln -s /opt/firefox/firefox /usr/bin/firefox-browser \
   && ln -s /usr/bin/headless-firefox /usr/bin/firefox \
   && rm "firefox-$FIREFOXBROWSER_VERSION.tar.bz2"

RUN mv /opt/google/chrome/google-chrome /opt/google/chrome/google-chrome-browser \
   && rm /usr/bin/google-chrome-stable \
   && rm /usr/bin/google-chrome \
   && ln -s /opt/google/chrome/google-chrome-browser /usr/bin/chrome \
   && ln -s /usr/bin/headless-chrome /usr/bin/google-chrome

RUN curl -SLO "https://chromedriver.storage.googleapis.com/$CHROMEDRIVER_VERSION/chromedriver_linux64.zip" \
  && unzip "chromedriver_linux64.zip" -d /usr/local/bin \
  && rm "chromedriver_linux64.zip"

RUN curl -SLO "https://github.com/mozilla/geckodriver/releases/download/v$GECKODRIVER_VERSION/geckodriver-v$GECKODRIVER_VERSION-linux64.tar.gz" \
  && tar zxvf "geckodriver-v$GECKODRIVER_VERSION-linux64.tar.gz" -C /usr/local/bin \
  && rm "geckodriver-v$GECKODRIVER_VERSION-linux64.tar.gz"

RUN pip install robotframework robotframework-selenium2library

COPY ./wait-for-it.sh /

RUN firefox-browser --version
RUN chrome --version
