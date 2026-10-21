
*Git :-*

    -> Git is a version control system  which control the code changes in our system.

    -> Git tracks snapshot of the project and then store it efficently by using unchanged files at each commit.

    -> Git is a DVCS(Ditributed version control system).
        Every Developer has the compelete copy of the reposatory incuding commit history , branches and metadataon their own machine.
        

    -> Git is a Software which is locally installed on our systems. Available for Windows , macOS and Linux  

    -> Back Days system used by devs for version control where called as SCCS(Source Code Control System) which was closed source and required licensing for use expensive and not so user-friendly in nature.


    -> Git Architeure : 

                A. Working Directory(Project Folder)
                            |
                            |
                            ⌄ 
                B.  Git Staging Area(.git/index)
                            |
                            |
                            ⌄
                C.  Local Reposatory(.git folder)
                            |
                            |
                            ⌄ 
                D.  Remote Reposatory

                
        A. Working Directory: 

            $ This is the folder where we create files modify the files and write our code into the files locally in our system.

        B. Git Staging Area : 

            $ A special area provided by git for those files which are ready to be commited in the next commit.

            $ A temparary area which holdes files which are ready for commit.
        
        C. Local Reposatory :

            $ .git folder is the git Local Reposatory which store the different version of our source code in efficent manner.

        D. Remote Reposatory :

            $ This is the online hosted reposatory of git. provided by different organizations most famous and widly used one is github , gitlabs and bitbucket etc.

            $ To push changes to this reposatory we need internet as we need to communicate with the server.

    -> .git folder :

        now what is this .git folder what things are inside this folder and how this folder alone do the work of version control of our source code.

        $ Structure of this .git folder :

            Default files :

            1. hooks(directory)
            2. info(directory)
            3. objects(directory)
            4. refs(directory)
            5. config(file)
            6. description(file)
            7. HEAD(file)
            8. index(stagging area)
            9. logs

        
        @ Behind the sence of .git :- 

        -> how git actully work will see in this section : 

            so when ever we initialize a git reposatory git creates .git folder which store all the version of our code in the efficent manner in this hidden .git folder.

            now how actully it store this stuff in it is something we gonna learn in this section 

            so basically git is storing the info in the objects inside the object folder of .git 

            now types of objects git use are :

                1. Blob
                2. commit
                3. tree
                4. tag

            now we will see the segnificance of each object in git echosystem:

            & Blob :- so Blob is basically binary large object which store the content of the file. 

            & commit :- commit is basically storing 
                A. commit message 
                B. Author 
                C. Timestamp
                D. Parent commit 
                E. reference to tree
                F. commiter
                G. commiter timestamp
            
            & Tree :- tree represents directory structure 

                it stores : 
                    A. File Name
                    B. Folder Name
                    C. reference to blob
                    D. reference to other tree
            
            & Tag :- A Tag is a lable attaced to specfic commit 

                Ex - v1.0
                    git tag v1.0


        @ git References : /refs (folder) :

            # now what is reference in git it is a simple .txt file with SHA-1 hash in it of commits to keep the track of commits

            now this .txt files are mainly of three types :
                a). branchname
                b). tagname
                c). HEAD
            

            # and the .txt file is actuly the name of branch of that commit
            a branch which points to that commit


            ex .git/refs/heads/<branch.txt> -> hash of the commit will be there in this file


        @ git branch : 

            a branch is reference file which store the latest commit hash on that branch


            ex refs/heads/master --> hash of latest commit

            once we commit the changes the hash is updated with the latest commit 
        
        @ HEAD :-> 

            HEAD is special reference which store what is currenlty checked out  

            HEAD file -> refs/heads/master --> hash of commit

            or sometimes just the direct hash of the commit

            and when this thing happen usually HEAD point to branch 

            defualt case : HEAD -> Branch -> commit

            now will se the second case 
        
        @Detached HEAD :

            now in this HEAD directly point to commit there is no branch in this case 

            ex : HEAD -> commit hash

            so when we are in this state if we make changes then to keep those changes we need to create a branch(a txt file to store this hash of commit) else once we switch to latest commit those changes are in the .git but we dont have an pointer pointing to that commit hash so called a branch .

        @Tags refs/tags : 

            tags are pointers which point to spesific commit in the git history 

            tags are prementent and they dont change.

            there exist 2 types of tags : 
                1. lightwegith tags -> store only hash of spesific commit 
                2. annoted tags -> sotre hash as well as the commit meta data such as 
                    1. commiter 
                    2. mesg 
                    3. timestamp

            Annoted Tag -> Tag object(we seen this above is actully creted to store this info of commit meta data then used) --> commit;


        @ Actual working of git :

            now when we  execute the commands git start its work 

            how we actully use the git : 

            % Step 1: initilize the folder with git 

                command : git init

            % Step 2: create files in the folder 
                
                command : echo "example file" > file.txt 

            % Step 3: add those files to staging area 

                command : git add <filename> or .

            **-> now when we execute this command git internally create an Blob object which store the content of the file.txt just the content nothing else than that .(not for files which are unchaged)

            % Step 4 : commiting the changes made by us 

                command : git commit -m "message"

            **-> now this time git create two objects 
                1. tree (which store the structure of the files)

                2. commit (which store the meta data of the commit ex Auther , commit mesg , timestamp , reference to tree , and parent commit info)
            
            and then finally our first commit is done . :) 

            $ So this was some thing we should know before we use git

<br> 


    -> Git basic commands : 

        1. git init - initilazing a git reposatory 
        2. git add  - to add a file in to the staging area .
        3. git commit - to commit the changes and create a check point or we could say a version of our system.   
<br>

    -> Git Advance Commands : <Super important topic>

        now as a dev we should know this all commands because this are the commands which will help in our development 

        $ git log : <looks small but the most complex command as well most usefull>
         # now this command git log will show us details about the commit history 

         ex - Auther name 
              timestamp 
              commit msg
        
        now will see the various flags for git log for more easer understanding of commit history

        1) --oneline : now this will give us all commit details in one line small and easer for understanding

        2) --reverse : now usually git show commit history in reverse order latest to oldest at bottom and we sometimes are not familiour with this order so to get it like from old to latest we use --reverse flag

        3) --pretty=format:<"placeholder"> : now this flag give us an option format the logs according to our needs 

            placeholder: 
             a) %H -> full commit hash
             b) %h -> short commit hash
             c) %an -> auther name
             d) %ae -> auther email
             e) %ad -> auther date
             f) %s -> commit mesg
             g) %cn -> committer name 

        ex - git log --pretty=format:"%h | %an | %s "
            output hash | authername | commit mesg

        Color coustomiztion :
        placeholder : 
        a) %C -> apply color 
        b) %Creset -> after this placeholder color will rest to defult 

        ex -> git log --pretty=format:"%Cyellow%h%Creset | %an | %s "

        now hash will be in the yellow color for each log rest in default

        $git log --after :

        so in this after provide the commit made after a spesific date 

        ex :- git log --after="date" 
                git log --after="9 days ago"
                git log --after="yyyy-mm-dd"
        
        $git log --before :

            git log --before="time"
            git log --before="yeasterday"
            git log --before="9 days ago"

        $ use of both after and before: <creating the range>

        git log --oneline --after="5 days ago" --before="5 days ago"

        $ git log --graph : 

        now this command show us the commit in the tree structure which gives us an more clear image of commit history

        ex - git log --graph --oneline --all

        $git reflog :

            now thorugh this command we can see where our HEAD has referenced 

            git reflog

            Example:

        658c7c7 HEAD@{0}: checkout
        12ac218 HEAD@{1}: commit
        954b260 HEAD@{2}: checkout

    -> git configuration : <change git us your usecase>
