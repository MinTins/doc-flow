FROM node:20-alpine

WORKDIR /usr/src/app

COPY package.json package-lock.json* ./
RUN npm ci || npm install

COPY . .

# Create entrypoint script with guaranteed Unix line endings
RUN cat > /usr/src/app/entrypoint.sh <<'EOF'
#!/bin/sh
set -e

if [ ! -d node_modules ]; then
  npm install
fi

npm run dev -- --host 0.0.0.0 --port 5173
EOF

RUN chmod +x /usr/src/app/entrypoint.sh

EXPOSE 5173

CMD ["/bin/sh", "/usr/src/app/entrypoint.sh"]


