#FROM node:20 AS builder 

#WORKDIR /builder

#COPY . /builder

#RUN npm install \
#    && npm run build 


#FROM lipanski/docker-static-website:2.4.0

#WORKDIR /home/static

#COPY  --from=builder /builder/dist/apps/web/  /home/static

#EXPOSE 80

#CMD ["/busybox-httpd", "-f", "-v", "-p", "80", "-c", "httpd.conf"]


# ---------- Build stage ----------
FROM node:20-alpine AS builder

# أدوات لازمة لبعض مشاريع Nx أثناء البناء
RUN apk add --no-cache git

WORKDIR /builder

# انسخ ملفات lock/manifest فقط أولاً للاستفادة من طبقات الكاش
COPY package.json ./
COPY package-lock.json* ./
COPY pnpm-lock.yaml* ./
COPY yarn.lock* ./

# فعّل corepack عشان pnpm/yarn لو الريبو بيستخدمهم
RUN corepack enable || true

# ثبّت اعتمادًا على نوع الـ lockfile
RUN if [ -f pnpm-lock.yaml ]; then pnpm i --frozen-lockfile; \
    elif [ -f yarn.lock ]; then yarn install --frozen-lockfile; \
    elif [ -f package-lock.json ]; then npm ci; \
    else npm install; fi

# الآن انسخ بقية السورس
COPY . .

# Nx أحيانًا يعلّق في Docker لو الـ daemon شغّال
ENV NX_DAEMON=false

# ابنِ كل التارغتس المطلوبة
# استخدم السكربت المعرّف في package.json أو نفّذ nx مباشرة
# جرّب أولاً السكربت:
RUN if npm run | grep -qE '(^| )build( |:)'; then npm run build --if-present; \
    else npx nx run-many -t=build --skip-nx-cache; fi


# ---------- Runtime stage ----------
FROM lipanski/docker-static-website:2.4.0

WORKDIR /home/static

# عدّل المسار حسب مخرجات البناء الفعلية في مشروعك
COPY --from=builder /builder/dist/apps/web/ /home/static

EXPOSE 80
CMD ["/busybox-httpd", "-f", "-v", "-p", "80", "-c", "httpd.conf"]
