FROM python:alpine
RUN pip install --no-cache-dir Radicale[bcrypt]
EXPOSE 5232/tcp
VOLUME /var/lib/radicale
ENTRYPOINT ["radicale", "-H", "0.0.0.0:5232"]
