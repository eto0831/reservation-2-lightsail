FROM php:8.1-fpm

# 必要なツールと拡張機能をインストール
RUN apt-get update -o Acquire::http::Timeout="600" -o Acquire::Retries="5" \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
      supervisor \
      default-mysql-client \
      zlib1g-dev \
      libzip-dev \
      unzip \
      libpng-dev \
      tzdata \
      cron \
  && docker-php-ext-install pdo_mysql \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*


# タイムゾーン設定
ENV TZ=Asia/Tokyo

# 作業ディレクトリ
WORKDIR /var/www

# SchedulerスクリプトとSupervisor設定を追加
COPY scheduler.sh /usr/local/bin/scheduler.sh
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN chmod +x /usr/local/bin/scheduler.sh
