docker-lastpass-cli

An Alpine 3.7 image with the lpass command line tool installed.

Examples

./lpass-show --notes somesecret | pbcopy
Email: foo@bar.com
Success: Logged in as foo@bar.com.
echo $(pbpaste)
some super secret

docker run -itd --name lastpass-cli mbigras/lastpass-cli
docker exec -it lastpass-cli lpass login foo@bar.com
docker exec lastpass-cli lpass show --notes somesecret
some super secret
echo another super secret | docker exec -i lastpass-cli lpass add --sync now --non-interactive --notes anothersecret
docker exec lastpass-cli lpass show --notes anothersecret
another super secret

Gotcha

Be careful of using the -t, --tty switch when printing to stdout because a return character will get inserted.
For example:

docker exec -t lastpass-cli lpass show --notes anothersecret | od -A d -c
0000000    a   n   o   t   h   e   r       s   u   p   e   r       s   e
0000016    c   r   e   t  \r  \n
0000022

docker exec lastpass-cli lpass show --notes anothersecret | od -A d -c
0000000    a   n   o   t   h   e   r       s   u   p   e   r       s   e
0000016    c   r   e   t  \n
0000021



Links

https://pkgs.alpinelinux.org/package/edge/community/x86/lastpass-cli
https://github.com/lastpass/lastpass-cli
