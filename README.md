# Flask-DockerCICD

****Create and build the Docker image****

1- Create a file named `Dockerfile` and add the following content:

```
FROM python:3.6.1-alpine
RUN pip install flask
CMD ["python","app.py"]
COPY app.py /app.py
```
- Build the Docker image. Pass in the `-t`
 parameter to name your image python-hello-world.
 
```
 docker image build -t python-hello-world .
```
<img width="786" alt="DockerImageBuild" src="https://user-images.githubusercontent.com/57734887/230778845-6ce58d92-db71-4007-abc2-b3267d5d24bf.png">

- Verify that your image shows in your image list:

```
 docker image ls
```

2- Run the Docker image

```
docker run -p 5001:5000 -d python-hello-world
```
Navigate to http://localhost:5001 in a browser to see the results.
<img width="636" alt="dockerRunImage" src="https://user-images.githubusercontent.com/57734887/230778853-8c81f669-2394-428c-8853-4c9538fc0979.png">


- Check the log output of the container.
```
docker container ls
```
```
docker container logs [container id]
```

3-Push to a central registry
-Log in to the Docker registry account by entering docker login
 on your terminal:
 ```
 docker login
```

Tag the image with your username.
```
docker tag python-hello-world [dockerhub username]/python-hello-world
```

After you properly tag the image, use the docker push
 command to push your image to the Docker Hub registry:
```
 docker push redmal/python-hello-world
```
<img width="670" alt="dockerPushImage" src="https://user-images.githubusercontent.com/57734887/230779721-488dbbf1-a8fd-4c6f-8910-196f8b4820a4.png">

Check your image on Docker Hub in your browser.
<img width="641" alt="dockerHub" src="https://user-images.githubusercontent.com/57734887/230779744-d4d53701-6e24-4f55-939b-a408e33053d9.png">

4-Deploy a change
-Update app.py by replacing the string "Hello World" with "Hello Beautiful World!" in app.py.
Your file should have the following contents:

```python

from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello Beautiful World!"


if __name__ == "__main__":
    app.run(host='0.0.0.0')
```

Now that your application is updated, you need to rebuild your app and push it to the Docker Hub registry.

-Rebuild the app by using your Docker Hub username in the build command:
```
docker image build -t redmal/python-hello-world .
```
<img width="670" alt="DockerRebuild" src="https://user-images.githubusercontent.com/57734887/230780171-6f1c168f-7860-4716-b01a-6eed0de36413.png">

Notice the "Using cache" for Steps 2-3. These layers of the Docker image have already been built, and the docker image build
command will use these layers from the cache instead of rebuilding them.

```
docker push redmal/python-hello-world
```
<img width="590" alt="dockerPushRebuildImg" src="https://user-images.githubusercontent.com/57734887/230780258-c27fae5e-c3ca-4aef-a27c-1f065d94acc6.png">





