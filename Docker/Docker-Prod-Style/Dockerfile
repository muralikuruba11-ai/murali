# 1. Base image with Python
FROM python:3.11-slim

# 2. Image metadata
LABEL maintainer="murali@example.com"
LABEL version="1.0"
LABEL description="Python Flask Docker Application"

# 3. Environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV APP_HOME=/app

# 4. Set working directory
WORKDIR $APP_HOME

# 5. Update OS packages
RUN apt-get update

# 6. Install system dependencies
RUN apt-get install -y \
    gcc \
    curl \
    vim

# 7. Clean apt cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# 8. Copy dependency file
COPY requirements.txt .

# 9. Upgrade pip
RUN pip install --upgrade pip

# 10. Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# 11. Copy application code
COPY . .

# 12. Create application user
RUN groupadd appgroup && useradd -m -g appgroup appuser

# 13. Set permissions
RUN chown -R appuser:appgroup $APP_HOME

# 14. Switch to non-root user
USER appuser

# 15. Expose application port
EXPOSE 5000

# 16. Health check
HEALTHCHECK CMD curl --fail http://localhost:5000 || exit 1

# 17. Start application
CMD ["python", "app.py"]
