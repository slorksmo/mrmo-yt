هتحتاج تعمل DB جديدة لـ n8n بنفس الطريقة من Adminer:

sql
Copy
Edit
CREATE DATABASE n8n_db;
CREATE USER n8n_user WITH ENCRYPTED PASSWORD 'StrongN8nPass123';
GRANT ALL PRIVILEGES ON DATABASE n8n_db TO n8n_user;
هيفتح على http://SERVER_IP:5678

# n8n folder dirctory
mkdir -p /home/mrmo/n8n_stack/data
cd /home/mrmo/n8n_stack
docker compose up -d
