FROM nginx:latest

COPY docker/nginx/conf.d/ /etc/nginx/conf.d
COPY . /var/www

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]