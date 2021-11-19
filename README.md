# Thông báo qua telegram khi truy cập qua ssh
## Tạo bot telegram
Chat với @BotFather trên Telegram
<ảnh bot>
Chọn /newbot
Chọn namebot sau đó tên bot hiển thị
Tạo file chưa script /etc/ssh/sshrc
'USERID="-687425017"
KEY="2121672410:AAHmMSvdZHyJsh-1HX7YnVIJo7nw5Bb12o0"
TIMEOUT="10"
URL="https://api.telegram.org/bot$KEY/sendMessage"
DATE_EXEC="$(date "+%d %b %Y %H:%M")"
TMPFILE='/tmp/ipinfo-$DATE_EXEC.txt'
if [ -n "$SSH_CLIENT" ]; then
        IP=$(echo $SSH_CLIENT | awk '{print $1}')
        HOSTNAME=$(hostname -f)
        IPADDR=$(hostname -I | awk '{print $1}')
        curl http://ipinfo.io/$IP -s -o $TMPFILE
        TEXT="$DATE_EXEC  User: ${USER} logged in to server $HOSTNAME $IPADDR from source-ip: $IP"
        curl -s --max-time $TIMEOUT -d "chat_id=$USERID&disable_web_page_preview=1&text=$TEXT" $URL > /dev/null
fi'
