# PhotoblogOmegaProject
What is making me sad - Photoblog is dying slowly and unavoidably and there's nothing we can do to stop the decay. There are people who put a lot of memories(like there are some people with 8000+ posts - good luck downloading that manually) and content - there's however no way to bulk download the contents. 

Here's the solution to the issue. Now You can save Your own memories from being forgotten in the digital abyss.

                    ##################
                    ### DISCLAIMER ###
                    ##################

This readme is for non-very-it-people, thus it's written the way it is. Please, be understanding, umkhay?

                    ##################################################################
                    ########## INSTALLATION OF PYTHON AND THE PREREQUISITES ##########
                    ##################################################################

The script requires installed Python 3.x and some additional libraries (available in the public repo). Here's what You need to do:
  1) Download official release of Python from the absolutely official website - here: https://www.python.org/downloads/ and install it (REMEMVER TO ADD IT TO THE PATH, it should be a part of installation process)
  2) Once the Python is up and running start command prompt (just type CMD in search bar and start it)
  3) Run those commands(just copy paste it into command prompt):
  
          a)python --version
              WHY: To check if the Python is installed correctly.
              RESPONSE: Python 3.x.x (obviously those x'es will be numbers)
              NO RESPONSE OR EVEN WORSE- AN ERROR! - You probably didn't add Python to PATH! Uninstall Python and install it again.
          b)pip --version
              WHY: To check if the pip is installed correctly - You'll need it to install the packages
              RESPONSE: pip xx.x.x from c:\users\****\appdata\local\programs\python\python38\lib\site-packages\pip (python 3.8)
              NO RESPONSE OR EVEN WORSE- AN ERROR! - You probably didn't install pip together with Python. If You've read carefully what I've written above You already know the solution to that one.
          c) pip install requests
                    WHY: The script needs that library to make the connection to the webpage and suck down the source code.
          d) pip install bs4
                    WHY: The script needs that library to understand the source code and get the information You need.
          e) pip install beautifulsoup
                    WHY: Same as above.

Once Python and the libraries are in place You can download the PhotoblogOmegaProject.py file to Your PC.

Once You downloaded it OPEN IT WITH A TEXT EDITOR. I don't care if it's notepad, notepad++ or IDLE (I'll explain in a moment, but I'd prefer You do it in IDLE).

Now You have to make some changes to the code there.

Find this line:
      ########## \/ MODIFY THIS  \/ ##########

and modify those lines:

        filesDrop_main = "FILLMEEEEEEE"
        URL_userName = "FILLLMEEEETOOOOO"

filesDrop_main is a parent directory where the files will be downloaded. There's a catch here. Use double "\" when writing the address, 
i.e. d:\\\cojarobiezeswoimzyciem\\\olaboga\\\tutejbendommojepliczkihihihihi

URL_userName is Your photoblog's account name.

Do not modify anything else if You do not know what You're doing. Seriously. Don't.

Also, do not modify anything below that line:

        ########## \/ DO NOT MODIFY THIS \/ ##########
        ##########   SERIOUSLY, DO NOT!     ##########

Now all You have to do is run the script. There are two ways to do it and here's the easy one:

  1) Open IDLE. IDLE comes together with Python package. IDLE is kind of IDE (Integrated Development Environment). It allows You to run Python shell (where You can type code) or write scripts and even... MODIFY THEM! YES! MODIFY.
  2) Ok, now seriously open IDLE.
  3) FILE => OPEN
  4) Open the file (PhotoblogOmegaProject.py) You've just downloaded (id You didn't copy-paste it from the github)
  5) Make the modifications if You haven't already.
  6) Double check the modificaions You've made.
  7) Tripple check won't hurt.
  8) If You are sure that there are no typos proceed,
  9) RUN => RUN MODULE.
  10) Sit back and admire the magic happening.

Second option is running the script from command prompt: here's some tutorial made my an Indian guy: https://www.youtube.com/watch?v=gjBRlP0jKVk

                    ###########################################
                    ########## IMPORTANT INFORMATION ##########
                    ###########################################

IT WORKS ONLY ON WINDOWS. If You have Linux or Mac OS - that script probably won't help You. I did not test it in on any linux-based OSs.

IT WORKS WITH ALL THE LAYOUT OPTION - that was real pain in the arse.

YOU CAN RESTART IT ANY MOMENT, JUST PUT the last downloaded post number in URL_postNumber field in the code. Or skip it - the download process will omit already downloaded posts.

MOST LIKELY I'LL UPDATE THE SCRIP IN NEAR FUTURE. I'VE GOT SOME GOOD IDEAS I WANT IMPLEMENTED.

IT IS IMPOSSIBLE TO DOWNLOAD THE PASSWORD PROTECTED CONTENT. IF YOUR BLOG IS PASSWORD PROTECTED - TURN IT OFF FOR THE TIME OF DOWNLOAD.

                                                        ######################################################
                                                        ########### THE MOST IMPORTANT INFORMATION ###########
                                                        ######################################################
                                                        ## I know that this script will allow the download  ##
                                                        ## of absolutely any photoblog profile that is      ##
                                                        ## public. I really do, however, trust Your         ##
                                                        ## judgement and common sense not to abuse it's     ##
                                                        ## original purpose - that is - to download only    ##
                                                        ## the content that belongs to You.                 ##
                                                        ##     I understand, that having such "power" may   ##
                                                        ## corrupt weak willed people. Heed the warning     ##
                                                        ## then: DOWNLOAD ONLY WHAT'S YOURS...              ##
                                                        ##            ...OR I'LL REMOVE THE SCRIPT FOREVER  ##
                                                        ######################################################
                                                        ######################################################
















