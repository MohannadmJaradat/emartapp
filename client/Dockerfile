# muli stage docker file, first stage is to build the artifact, and the second one is to copy the artifact into
# our main image (nginx) and use it.

# Angular application will be built on node image
FROM node:14 AS web-build
WORKDIR /usr/src/app
COPY ./ ./client
RUN cd client && npm install && npm run build --prod

# Use official nginx image as the base image
FROM nginx:latest

# Copy the build output to replace the default nginx contents.
COPY --from=web-build /usr/src/app/client/dist/client/ /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 4200
EXPOSE 4200
