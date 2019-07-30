This is a project using baseball statistics from http://www.kaggle.com/.
The goal of the project is to find a roster of the players with the best on-base-percentage (OBP) for their salary.
This exercise uses the pandas package to analyze the data.

1.1 Introduction

This database contains pitching, hitting, and fielding statistics for
Major League Baseball from 1871 through 2014.  It includes data from
the two current leagues (American and National), the four other "major" 
leagues (American Association, Union Association, Players League, and
Federal League), and the National Association of 1871-1875. 

This database was created by Sean Lahman, who pioneered the effort to
make baseball statistics freely available to the general public. What
started as a one man effort in 1994 has grown tremendously, and now a
team of researchers have collected their efforts to make this the
largest and most accurate source for baseball statistics available
anywhere. (See Acknowledgements below for a list of the key
contributors to this project.)

None of what we have done would have been possible without the
pioneering work of Hy Turkin, S.C. Thompson, David Neft, and Pete
Palmer (among others).  All baseball fans owe a debt of gratitude
to the people who have worked so hard to build the tremendous set
of data that we have today.  Our thanks also to the many members of
the Society for American Baseball Research who have helped us over
the years.  We strongly urge you to support and join their efforts.
Please vist their website (www.sabr.org).

1.2:Steps to be followed

1.Select columns you want,retrieve the data from Batting.csv.
2.Select columns you want,retrieve the data from People.csv.
3.Select columns you want,retrieve the data from Salaries.csv.
4.Select columns you want,retrieve the data from Fielding.csv.
5.Merge Batting and People to get all data.
6.Merge All data and fielding.
7.Merge All data and Salaries.
8.If there is no not available data present copy all data.
9.If there is not available data Drop them.
10.If there are duplicates drop them.
11.OBP Formula, new column.
	This formula gives totally a differnt scenario of data
	***all_data_no_na['OBP'] = (all_data_no_na['H']+all_data_no_na['BB']+all_data_no_na['HBP'])/(all_data_no_na['AB']+all_data_no_na['BB']+all_data_no_na['HBP']+all_data_no_na['SF'])***
	a.OBP=ON-Base Percentage.
	b.H=Home Runs Per Hit.
	c.BB=Pitcher's ability to control pitches,calculated as Strikeouts divided by Bases On Balls.
	d.HBP=Hits By Pitch.
	e.AB=At bats per home run,at bats divided by home runs.
	f.SF=Sacrifice Flies.

12.All_data_no_na['Ratio'] = all_data_no_na['OBP']/all_data_no_na['salary']
	->For finding ratios of NO Not available data divide na of OBP by na of salary.
13.Moneyball = all_data_no_na[all_data_no_na['AB']>30]
	->At batting home runs/at bats divided by home runs of no not available columns.
14.Moneyball.sort_values('Ratio', ascending=False).head() 
	->sort values in order to find ratio and give whole data.
15.Moneyball.describe() 
	->To get count,mean,std,min,max,25%,50%,75%.
16.Retrieve New Salaries.
17.moneyball['OBP'].describe() 
	->To get count,mean,std,min,max,25%,50%,75%,type.
18.moneyball = moneyball.sort_values('Ratio', ascending=False)
	->sort values in descendiFng order by year and get ratios of all players.
19.moneyball.head(15) 
	->get all 15 players selected.
20.The above procedure is followed for solving MoneyBall.
21.Find accuracy of all algorithms and mean and SD Compare and get best algorithm.
outcome = []
model_names = []
models = [('LogReg', LogisticRegression()), 
          ('SVM', SVC()), 
          ('DecTree', DecisionTreeClassifier()),
          ('KNN', KNeighborsClassifier()),
          ('LinDisc', LinearDiscriminantAnalysis()),
          ('GaussianNB', GaussianNB())]
for model_name, model in models:
    k_fold_validation = model_selection.KFold(n_splits=10, random_state=random_seed)
    results = model_selection.cross_val_score(model, x, y, cv=k_fold_validation, scoring='accuracy')
    outcome.append(results)
    model_names.append(model_name)
    output_message = "%s| Mean=%f STD=%f" % (model_name, results.mean(), results.std())
    print(output_message)
22.Compare all algorithms.
fig = plt.figure()
fig.suptitle('Machine Learning Model Comparison')
ax = fig.add_subplot(111)
plt.boxplot(outcome)
ax.set_xticklabels(model_names)
plt.show()

1.3 Acknowledgements

Much of the raw data contained in this database comes from the work of
Pete Palmer, the legendary statistician, who has had a hand in most 
of the baseball encylopedias published since 1974. He is largely 
responsible for bringing the batting, pitching, and fielding data out
of the dark ages and into the computer era.  Without him, none of this
would be possible.  For more on Pete's work, please read his own 
account at: http://sabr.org/cmsfiles/PalmerDatabaseHistory.pdf

Three people have been key contributors to the work that followed, first 
by taking the raw data and creating a relational database, and later 
by extending the database to make it more accesible to researchers.

Sean Lahman launched the Baseball Archive's website back before 
most people had heard of the world wide web.  Frustrated by the
lack of sports data available, he led the effort to build a 
baseball database that everyone could use. Baseball researchers 
everywhere owe him a debt of gratitude.  Lahman served as an associate
editor for three editions of Total Baseball and contributed to five
editions of The ESPN Baseball Encyclopedia. He has also been active in
developing databases for other sports.

The work of Sean Forman to create and maintain an online encyclopedia
at "baseball-reference.com" has been remarkable. Recognized as the 
premier online reference source, Forman's site provides an oustanding
interface to the raw data. His efforts to help streamline the database
have been extremely helpful. Most importantly, Forman has spearheaded
the effort to provide standards that enable several different baseball
databases to be used together. He was also instrumental in launching
the Baseball Databank, a forum for researchers to gather and share
their work.

Since 2001, these two Seans have led a group of researchers
who volunteered to maintain and update the database. 

Ted Turocy has done the lion's share of the work to updating the main
data tables since 2012, including significant imporvements to the
demographic data in the master table. In his role as SABR data czar,
he led the effort to document college playing stints for all
major league players. Turocy also spearheads the Chadwick Baseball
Bureau. For more details on his tools and services, visit:
http://chadwick.sourceforge.net/doc/index.html  

A handful of researchers have made substantial contributions to 
maintain this database over years. Listed alphabetically, they 
are: Derek Adair, Mike Crain, Kevin Johnson, Rod Nelson, Tom Tango,
and Paul Wendt. These folks did much of the heavy lifting, and are 
largely responsible for the improvements made since 2000.

Others who made important contributions include: Dvd Avins, 
Clifford Blau, Bill Burgess, Clem Comly, Jeff Burk, Randy Cox, 
Mitch Dickerman, Paul DuBois, Mike Emeigh, F.X. Flinn, Bill Hickman,
Jerry Hoffman, Dan Holmes, Micke Hovmoller, Peter Kreutzer, 
Danile Levine, Bruce Macleod, Ken Matinale, Michael Mavrogiannis,
Cliff Otto, Alberto Perdomo, Dave Quinn, John Rickert, Tom Ruane,
Theron Skyles, Hans Van Slooten, Michael Westbay, and Rob Wood.

Many other people have made significant contributions to the database
over the years.  The contribution of Tom Ruane's effort to the overall
quality of the underlying data has been tremendous. His work at
retrosheet.org integrates the yearly data with the day-by-day data,
creating a reference source of startling depth. It is unlikely than 
any individual has contributed as much to the field of baseball 
research in the past five years as Ruane has.

Sean Holtz helped with a major overhaul and redesign before the
2000 season. Keith Woolner was instrumental in helping turn
a huge collection of stats into a relational database in the mid-1990s.
Clifford Otto & Ted Nye also helped provide guidance to the early 
versions. Lee Sinnis, John Northey & Erik Greenwood helped supply key
pieces of data. Many others have written in with corrections and 
suggestions that made each subsequent version even better than what
preceded it. 

The work of the SABR Baseball Records Committee, led by Lyle Spatz
has been invaluable.  So has the work of Bill Carle and the SABR 
Biographical Committee. David Vincent, keeper of the Home Run Log and
other bits of hard to find info, has always been helpful. The recent
addition of colleges to player bios is the result of much research by
members of SABR's Collegiate Baseball committee.

Salary data was first supplied by Doug Pappas, who passed away during
the summer of 2004. He was the leading authority on many subjects, 
most significantly the financial history of Major League Baseball. 
We are grateful that he allowed us to include some of the data he 
compiled.  His work has been continued by the SABR Business of 
Baseball committee.  

Thanks is also due to the staff at the National Baseball Library
in Cooperstown who have been so helpful over the years, including
Tim Wiles, Jim Gates, Bruce Markusen, and the rest of the staff.  

A special debt of gratitude is owed to Dave Smith and the folks at
Retrosheet. There is no other group working so hard to compile and
share baseball data.  Their website (www.retrosheet.org) will give
you a taste of the wealth of information Dave and the gang have collected.

Thanks to all contributors great and small. What you have created is
a wonderful thing.

Conclusion:
Using OBP OOBP train the data find the best algorithm by comparision.

References:
www.kaggle.com
https://en.wikipedia.org/wiki/Moneyball_(film)