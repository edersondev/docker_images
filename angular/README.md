# Image with Nodejs, Typescript and Angular-cli on Ubuntu

You can create yours projects using angular-cli and run ng-server.

To use:
```
docker run -it --rm -v "$PWD":"$PWD" -w "$PWD" -u "$(id -u)" edersondev/angular-cli ng
```