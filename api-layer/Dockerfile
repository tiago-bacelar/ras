# Use the official OpenResty Alpine image as the base image
FROM openresty/openresty:alpine

# Install Perl
RUN apk --no-cache add perl curl

RUN apk --no-cache add git && \
    git clone https://github.com/SkyLothar/lua-resty-jwt.git /tmp/lua-resty-jwt && \
    cp -r /tmp/lua-resty-jwt/lib/resty /usr/local/openresty/site/lualib && \
    git clone https://github.com/jkeys089/lua-resty-hmac.git /tmp/lua-resty-hmac && \
    cp -r /tmp/lua-resty-hmac/lib/resty /usr/local/openresty/site/lualib && \
    rm -rf /tmp/lua-resty-jwt && \
    rm -rf /tmp/lua-resty-hmac

# Copy your OpenResty configuration file to the container
COPY nginx.conf /usr/local/openresty/nginx/conf/nginx.conf
COPY lualib/* /usr/local/openresty/lualib

# Expose the necessary port (if different from the configuration)
EXPOSE 80
EXPOSE 8000

# Start OpenResty
CMD ["/usr/local/openresty/bin/openresty", "-g", "daemon off;"]
