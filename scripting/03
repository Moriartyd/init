#!/bin/bash
#Директория для бэкапа
BCKPDT=$HOME/backup_memory
BCKPD=$HOME/backup
#Все найденные файлы
FILE=files.all
#Скрипт для создания бэкап файла
BUSCRIPT=backup.script
#Скрипт для удаления ненужных файлов
RMSCRIPT=remove.script
ARHVNAME=backup.tar
rm -Rfv $BCKPDT $BCKPD 
mkdir $BCKPDT $BCKPD
du -a $HOME > $FILE
awk -F"/" '{print $NF}' $FILE | awk -F"." '{print $NF}' | sort | uniq -c | sort +0 -nr > result.txt
cat $FILE | grep 'tmp' | awk '{print "rm -Rf \047" $2"\047"}'> $RMSCRIPT
cat $FILE | grep 'tmp' | awk '{print "cp -Rf \047"$2 "\047 \047'$BCKPDT'\047"}'> $BUSCRIPT
cat $FILE | grep 'cache' | awk '{print "rm -Rf \047"$2"\047"}'>> $RMSCRIPT
cat $FILE | grep 'cache' | awk '{print "cp -Rf \047"$2 "\047 \047'$BCKPDT'\047"}'>> $BUSCRIPT
bash $BUSCRIPT
echo "tar -xvf $ARHVNAME" > $BCKPD/Backup.sh
cat $FILE | grep 'tmp' | awk '{print "cp -Rf " "\047" $NF "\047 \047"$2"\047"}'>> $BCKPD/Backup.sh
cat $FILE | grep 'cache' | awk '{print "cp -Rf " "\047" $NF "\047 \047"$2"\047"}'>> $BCKPD/Backup.sh
echo "cd\nrm -Rf $BCKPD" >> $BCKPD/Backup.sh
sh $RMSCRIPT
tar cf $ARHVNAME $BCKPDT
mv $ARHVNAME $BCKPD
rm -Rf $BCKPDT
rm -Rf $BUSCRIPT $RMSCRIPT
