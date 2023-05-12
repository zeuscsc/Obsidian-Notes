sudo kill -9 $(sudo lsof -t -i :7860 | sudo awk '{print $1}')
tail -f $(forever list | awk 'NR==3{gsub(/\033\[[0-9;]*m/,"",$9); print $9}')