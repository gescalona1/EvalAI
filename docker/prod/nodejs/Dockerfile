FROM node:8.11.2 as node

WORKDIR /code

# Add dependencies
ADD ./package.json /code
ADD ./bower.json /code
ADD ./gulpfile.js /code
ADD ./.eslintrc /code
ADD ./karma.conf.js /code

# Install Prerequisites
RUN npm install -g bower gulp@next
RUN npm install phantomjs-prebuilt
RUN npm link gulp
RUN npm cache clean -f
RUN npm install
RUN bower install --allow-root
ADD frontend /code/frontend

# TODO: Change `gulp dev` to `gulp prod`
RUN gulp prod
EXPOSE 8888

FROM nginx:1.13-alpine
COPY docker/prod/nodejs/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=node /code /code
