# Uses the Node image with latest tag to build the project.
FROM node:latest AS build

# Sets the working directory.
WORKDIR /usr/local/app

# Copies the entire application code to the working directory.
COPY ./ /usr/local/app/

# Installs dependencies using yarn.
RUN yarn

# Builds the application.
RUN npm run build

# Uses the latest Nginx image as the production stage.
FROM nginx:latest AS production

# Copies our custom Nginx configuration file.
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copies the built application from the build stage to the Nginx html directory.
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

# Exposes port 80 to allow external access.
EXPOSE 80