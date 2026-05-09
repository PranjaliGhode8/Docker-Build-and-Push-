FROM node:18-alpine AS base

WORKDIR /app

COPY package.json yarn.lock* package-lock.json* pnpm-lock.yaml* ./

RUN \
    if [ -f package-lock.json ]; then npm ci; \
    elif [ -f yarn.lock ]; then yarn --frozen-lockfile; \
    elif [ -f pnpm-lock.yaml ]; then corepack enable pmpm && pnpm install --frozen-lockfile; \
    else echo "No lockfile found" && exit 1; \
    fi

COPY . .

RUN npm run build

EXPOSE 3001

CMD ["npm","start"]
