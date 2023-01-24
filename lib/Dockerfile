FROM busybox

RUN mkdir -p /app/lib

RUN cat <<EOF > /app/lib/test
#/bin/bash
echo So, like, hello?
EOF

RUN chmod +x /app/lib/test

WORKDIR /app
