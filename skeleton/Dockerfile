# inherit from a existing image to add the functionality
FROM node:20.11.1
 
# Set the working directory
WORKDIR /app
 
# Copy the package.json and package-lock.json files into the image.
COPY package*.json ./
COPY prisma ./prisma
 
# Run the command to retrieve the IP address and set it as an environment variable
# RUN SERVER_IP=$(ip route get 1 | awk '{print $NF;exit}') && \
#     sed -i "s/localhost/$SERVER_IP/g" ./prisma/schema.prisma
 
# Set environment variable
ENV DATABASE_URL "mongodb+srv://root:root@nextecommerce.qrgzib9.mongodb.net/nextecommerce"
ENV NEXT_SECRET "wLc/H//eQxucJcFEScTpw1XfXg+NN0YwoQurJzZeGc8="
ENV API_URL "http://localhost:3000/"
ENV PUBLISHED_KEY "pk_live_51Ow0c3IoQMyf1cUgWH8FfX1MDIdr53UJRFy3YtaY3AQ80b674O6C36KIq53aQnCNbmmDa6riorXHyMU9zrOtQtxb00fofp70AT"
 
# Install the dependencies.
COPY . .
 
RUN npm install
RUN npm install -g prisma

RUN npm uninstall bcrypt
RUN npm i bcrypt

RUN npx prisma generate
RUN npm run build

RUN npx prisma db push
 
EXPOSE 3000
 
# Run the application.
CMD ["npm", "run", "dev"]