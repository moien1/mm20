# moein1
1.For visualisation dataset first I should create new container using the image ID of ubuntu
2.For save and share my file, I make sure that I have a github and then make public repository on github
3.I make 3 directories such data, gnuplot and R to push my dataset on data directory, plot my data with gnuplot and plot my data with R 
4.In my github you can see three directories:
  1.data: push my dataset and it's about a store that howmany products its sold.
  2.gnuplot2: I create 3 csv file that the first one is the firs week (first column) of my dataset in data directory and I named it sale1.csv and then plot the distibution it (sale1.png) , second one is the 51th week (51th column) of my dataset in data directory and then plot the distibution it (sale2.png) and the third one has 2 column (1st column + 51th column) and then plot it (sale3.png).
  3.R:I define my dataset as a variable y then I plot it with histogram and scatterplot. 
  
     ## IN THE BELOW YOU CAN SEE MY CODE ##

## start and attach ID container
marzieh$ docker start b64ae9de35f8
b64ae9de35f8
marzieh$ docker attach b64ae9de35f8

## Download local copy of github repository 
root@b64ae9de35f8:/# git clone http://github.com/moien1/moein1
... done.
root@b64ae9de35f8:/#ls
bin   dev  home  lib64  mnt     opt   root  sbin  sys  usr
boot  etc  lib   media  moein1  proc  run   srv   tmp  var

## change into github repository and create folder named "data"
root@b64ae9de35f8:/#cd moein1
root@b64ae9de35f8:/moein1# mkdir data
root@b64ae9de35f8:/moein1# ls
data

## copy dataset into new data folder
root@b64ae9de35f8:/moein1#exit
marzieh$ docker cp /Users/marzieh/Downloads/Sales_Transactions_Dataset_Weekly.csv b64ae9de35f8:/moein1/gnuplot2/Sales_Transactions_Dataset_Weekly.csv
marzieh$ docker start b64ae9de35f8
b64ae9de35f8
marzieh$ docker attach b64ae9de35f8
root@b64ae9de35f8:/#cd moein1
root@b64ae9de35f8:/moein1#cd data
root@b64ae9de35f8:/moein1/data# ls
Sales_Transactions_Dataset_Weekly.csv

## commit changes to github repository
root@b64ae9de35f8:/moein1/data# git add .
root@b64ae9de35f8:/moein1/data# git commit -am "upuploding data"
 Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'root@1b460c226ee7.(none)')

root@1b460c226ee7:/moein1/data# git config --global user.name "moien1"
root@1b460c226ee7:/compas/data# git config --global user.email "moien.marzieh@yahoo.com"

root@1b460c226ee7:/moein1/data# git commit -am "Uploading data"
[master d1968d6] Uploading data
 1 file changed, 1 insertion(+)
 create mode 100755 data/Sales_Transactions_Dataset_Weekly.csv

root@1b460c226ee7:/moein1/data# git push origin master
Username for 'https://github.com': moien1
Password for 'https://myi100@github.com':
Counting objects: 5, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 355 bytes | 0 bytes/s, done.
Total 4 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/moien1/moein1
   ca22e04..d1968d6  master -> master
root@1b460c226ee7:/moein1/data#


## create folder named "gnuplot2"
root@b64ae9de35f8:/#cd moein1
root@b64ae9de35f8:/moein1# mkdir gnuplot2
root@b64ae9de35f8:/moein1# ls
data gnuplot2

## copy my variables to my repository
marzieh$ docker cp /Users/marzieh/Downloads/sale1.csv b64ae9de35f8:/moein1/gnuplot2/sale1.csv
marzieh$ docker cp /Users/marzieh/Downloads/sale2.csv b64ae9de35f8:/moein1/gnuplot2/sale2.csv
marzieh$ docker cp /Users/marzieh/Downloads/sale3.csv b64ae9de35f8:/moein1/gnuplot2/sale3.csv
marzieh$ docker start b64ae9de35f8
b64ae9de35f8
marzieh$ docker attach b64ae9de35f8
root@b64ae9de35f8:/# cd moein1
root@b64ae9de35f8:/cd moein1# cd gnuplot2
root@b64ae9de35f8:/moein1/gnuplot2# ls
sale1.csv sale2.csv sale3.csv

## plot 2 variables with gnuplot
#Sale1 row is about products that store sold in the first week. Sale2 row is about products that store sold in the 51th week.

root@b64ae9de35f8:/moein1/gnuplot2# gnuplot


	G N U P L O T
	Version 4.6 patchlevel 4    last modified 2013-10-02 
	Build System: Linux x86_64

	Copyright (C) 1986-1993, 1998, 2004, 2007-2013
	Thomas Williams, Colin Kelley and many others

	gnuplot home:     http://www.gnuplot.info
	faq, bugs, etc:   type "help FAQ"
	immediate help:   type "help"  (plot window: hit 'h')

Terminal type set to 'unknown'

## plot the first week of dataset/ title=sale1/ xlabel=week/ ylabel=product 
gnuplot> set title '<sale1>'
gnuplot> set ylabel '<product>'
gnuplot> set xlabel '<week>'
gnuplot> set grid
gnuplot> set terminal png
Terminal type set to 'png'
Options are 'nocrop font "/usr/share/fonts/truetype/liberation/LiberationSans-Regular.ttf,12" fontscale 1.0 size 640,480 '
gnuplot> set output 'sale1.png'
gnuplot> bin_width= .1
gnuplot> bin_number(x)=floor(x/bin_width)
gnuplot> rounded(x)=bin_width * (bin_number(x) + 0.5)
gnuplot> set yrange [0:54]
gnuplot> plot 'sale1.csv' using (rounded($1)):(1) smooth frequency with boxes

## plot the 51th week of dataset/ title=sale2/ xlabel=week/ ylabel=product
gnuplot> set title '<sale2>'
gnuplot> set ylabel '<product>'
gnuplot> set xlabel '<week>'
gnuplot> set grid
gnuplot> set terminal png
Terminal type set to 'png'
Options are 'nocrop font "/usr/share/fonts/truetype/liberation/LiberationSans-Regular.ttf,12" fontscale 1.0 size 640,480 '
gnuplot> set output 'sale2.png'
gnuplot> bin_width= .1
gnuplot> bin_number(x)=floor(x/bin_width)
gnuplot> rounded(x)=bin_width * (bin_number(x) + 0.5)
gnuplot> set yrange [0:73]
gnuplot> plot 'sale2.csv' using (rounded($1)):(1) smooth frequency with boxes

## plot the first week  and the 51th week of dataset/ title=sale3/ xlabel=week/ ylabel=product
gnuplot> set title '<sale3>'
gnuplot> set ylabel '<product>'
gnuplot> set xlabel '<week>'
gnuplot> set grid
gnuplot> set terminal png
Terminal type set to 'png'
Options are 'nocrop font "/usr/share/fonts/truetype/liberation/LiberationSans-Regular.ttf,12" fontscale 1.0 size 640,480 '
gnuplot> set output 'sale3.png'
gnuplot> set datafile separator ","
gnuplot> plot 'sale3.csv' using 1:2 with lines

gnuplot> exit

## copy 3plots on my download folder
root@b64ae9de35f8:/moein1/gnuplot2# ls
sale1.csv sale1.png sale2.csv sale2.png sale3.csv sale3.png

root@b64ae9de35f8:/moein1/gnuplot2# exit
exit

marzieh$ docker cp b64ae9de35f8:/moein1/gnuplot2/sale1.png /Users/marzieh/Downloads/sale1.png
marzieh$ docker cp b64ae9de35f8:/moein1/gnuplot2/sale2.png /Users/marzieh/Downloads/sale2.png
marzieh$ docker cp b64ae9de35f8:/moein1/gnuplot2/sale3.png /Users/marzieh/Downloads/sale3.png

## commit changes to github repository
root@b64ae9de35f8:/moein1/gnuplot2# git add .
root@b64ae9de35f8:/moein1/gnuplot2# git commit -am "upuploding data"
root@1b460c226ee7:/moein1/gnuplot2# git push origin master
Username for 'https://github.com': moien1
Password for 'https://myi100@github.com':

###### #########################################################################################
## create folder named "R"
root@b64ae9de35f8:/#cd moein1
root@b64ae9de35f8:/moein1# mkdir R
root@b64ae9de35f8:/moein1# ls
data gnuplot2 R

## plot 2 variables with R
#define variable

library(RCurl)
y <- read.csv("https://raw.githubusercontent.com/moien1/moein1/master/data/Sales_Transactions_Dataset_Weekly.csv")


#plot histogram of the firs week/ color=red/ title=HISTOGRAM OF DATASET, limitation of x=(0,50),limitation of y=(0,100), lable of x= WEEKS, y label of y= PRODUCT 
hist(y$W1, col="RED", main="HISTOGRAM OF DATASET", xlim=c(0,50), ylim=c(0,100) , xlab="WEEKS", ylab="PRODUCT")

#plot histogram of the 51th week/ color=red/ title=HISTOGRAM OF DATASET, limitation of x=(0,50),limitation of y=(0,100), lable of x= WEEKS, y label of y= PRODUCT
hist(y$W51, col="RED", main="HISTOGRAM OF DATASET", xlim=c(0,50), ylim=c(0,100) , xlab="WEEKS", ylab="PRODUCT")

#plot scatterplot of the first & 51th week/ color=red/ title=SCATTERPLOT OF DATASET, lable of x= WEEKS, y label of y= PRODUCT
scatter.smooth(y$W1,y$W51, col="RED", main="SCATTERPLOT OF DATASET", xlab="WEEKS", ylab="PRODUCT")

## commit changes to github repository
root@b64ae9de35f8:/moein1/R# git add .
root@b64ae9de35f8:/moein1/R# git commit -am "upuploding data"
root@1b460c226ee7:/moein1/R# git push origin master
Username for 'https://github.com': moien1
Password for 'https://myi100@github.com':

