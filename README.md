Apline-nginx-livereload-injection
===

Nginx reverse proxy based on alpine, injecting livereload js snippet at each request.

## How to use
This image is designed to be used in association with a livereload container, and a directory to watch (`html/` in the example below).

- Create your `docker-compose.yml` (or copy the one contained in this repo) ;


    version: '2'
    
    services:
      nginx-proxy:
        image: cethy/apline-nginx-livereload-injection:v1.0
        ports:
          - "8008:80"
        volumes:
          - "./html:/usr/share/nginx/html"
    
      livereload:
        image: cethy/alpine-livereload:v1.0
        ports:
          - "35729:35729"
        volumes:
          - ./html:/usr/src/livereload-watch  # OUTPUT_DIR
        command: "/usr/src/livereload-watch -u true -d --exts 'css,js,html'"
        
- run `docker-compose` ;

    `docker-compose up -d`
    
- open your browser at [http://localhost:8008](http://localhost:8008) ;

- modify a file in your watched directory ;

- think about the time you just save. :)

## Limitations
- The nginx configuration is setup to inject the snippet only on html pages ;
- Only localhost configuration will work ;

You can however probably work around theses limitations by modifying the project.
