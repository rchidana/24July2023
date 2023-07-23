kubectl run busybox --image=busybox --dry-run=client -o yaml --command -- /bin/sh -c 'echo "hello world";sleep 1d'
