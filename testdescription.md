## Steps involved in running the container and testing the application
- Build the file with the command
 `docker build -t scatest:latest .`
- Run the container on port 8000 with the command
`docker run -d -p 8000:80 scatest:latest`
- Navigate to http://localhost:8000/ on the browser

![Output](/assets/output.png)