FROM python:3.9
WORKDIR /app
ADD . /app
EXPOSE 8081
# Install dependencies
RUN pip install redis

# Run the app
CMD ["python", "main.py"]