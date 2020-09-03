# -*- coding: utf-8 -*-

# just a reminder
# run those commands in the command prompt to install the required packages
# pip install requests
# pip install bs4

import requests
import datetime
from bs4 import BeautifulSoup
import os
import re
import csv

########## \/ MODIFY THIS  \/ ##########
filesDrop_main = "D:\\[KODZENIE]\\PhotoblogOmegaProject"
URL_userName = "pusjel"

########## \/ DO NOT MODIFY THIS \/ ##########
##########   SERIOUSLY, DO NOT!     ##########

URL_base = "https://www.photoblog.pl"
URL_postNumber = ""
href_val = "poprzednie »"

months = ["STY", "LUT", "MAR", "KWI", "MAJ", "CZE", "LIP", "SIE", "WRZ", "PAź", "LIS", "GRU"]
months2 = ["STYCZNIA", "LUTEGO", "MARCA", "KWIETNIA", "MAJA", "CZERWCA", "LIPCA", "SIERPNIA", "WRZEśNIA",
           "PAźDZIERNIKA", "LISTOPADA", "GRUDNIA"]

filesdrop_image = filesDrop_main+"\\"+URL_userName+ "\\" + "PHOTOS"
filesdrop_story = filesDrop_main+"\\"+URL_userName+ "\\" + "STORIES"
fullURL = URL_base + "/" + URL_userName + "/" + URL_postNumber
isok = 1
isLast = False
count = 0
log = []

print(filesDrop_main)
print(filesdrop_image)
print(filesdrop_story)

############## FUNCTIONS ##############

# Checks if the connection is working
def statusCheck(fullURL):
    try:
        response = requests.get(fullURL)
        if response.status_code == 200:
            success = True
            print("webpage", fullURL, "opened correctly")
        else:
            success = False
            print("webpage", fullURL, "Connection refused, response code", response)
    except:
        success = False
        print("Connection failure - incorrect address or page cannot be reached")
    return success
# TEST = OK

# Fetches the image.
def getPhoto(soup):
    try:
        photoLink = soup.find("meta", property="og:image")
        photo = photoLink.get("content", None)
        return photo
    except:
        print('error obtaining image address for property="og:image')
# TEST = OK

# You'll never guess. It downloads the photo!
def downloadPhoto(soup, filesdrop_image, listofscrapedphotos):
    photo = getPhoto(soup)
    date = getDate(soup)
    photoName = date+"_"+photo.split("/")[5]
    print(photoName)
    if not photoName in listofscrapedphotos:
        image = requests.get(photo).content
        with open(filesdrop_image+"\\"+photoName, 'wb') as temp:
            temp.write(image)
            temp.close()
        print("Downloading :", photo, "as :", photoName)
    else:
        print("image", photoName, "already exists in the directory")
# TEST = OK

# YES, that downloads the full post
def downloadPost(soup, listofscrapedstories):
    photo = getPhoto(soup)
    description = getDescription(soup)
    note = getNote(soup)
    title = getTitle(soup)
    date = getDate(soup)
    URL_postNumber = getPhoto(soup).split("/")[5].split(".")[0]
    postName = date+"_"+URL_postNumber+".txt"
    print(postName)
    if not postName in listofscrapedstories:
        with open(filesdrop_story+"\\"+postName, 'w', encoding="utf-8") as temp:
            temp.write(date+" | "+title+"\n\n")
            #temp.write(description)
            temp.write(note)
            temp.close()
        print("Downloading :", URL_postNumber, "as :", postName)
    else:
        print("post", postName, "already exists in the directory")
# TEST = OK

# Fetches the date, when needed parses it.
# Date format is YYYY_MM_DD
def getDate(soup):
    try:
        dateRAW = [item.get_text(strip=True) for item in soup.select("span.now_date")]
        dateTod = dateRAW[0].replace("/", "_")
        return dateTod
    except:
        try:
            if soup.find("span", {"class": "date"}).contents[0] == "Dodane ":
                dateTod = str(d.today())
                date = dateTod.replace("-", "_")
                return date
            elif soup.find("span", {"class": "date"}).contents[1] == " godz. temu":
                dateTod = str(d.today())
                date = dateTod.replace("-", "_")
                return date
            elif soup.find("span", {"class": "date"}).contents[0] in months:
                dateRAW = soup.find("span", {"class": "date"}).contents
                month = dateRAW[0]
                year = dateRAW[2].contents[0]
                day = dateRAW[1].contents[0]
                month = (monthCheck(month))
                date = year + "_" + month + "_" + day
                return date
            else:
                dateRAW = soup.find("span", {"class": "date"}).contents
                dateSep = dateRAW[0]
                dateSep = dateSep.split(" ")
                month = (monthCheck(dateSep[2]))
                date = dateSep[3] + "_" + month + "_" + dateSep[1]
                return date
        except:
            try:
                dateRAW = soup.find("span", {"class": "date"}).contents
                dateSep = []
                # print('dateraw split:', dateRAW[0].split())
                dateSep = dateRAW[0].split()
                month = (monthCheck(dateSep[2]))
                date = dateSep[3] + "_" + month + "_" + dateSep[1]
            except:
                date = "n/a"
            return date
# TEST = OK

# Support function for parsing the month at newer date formats / "MoDeRn LaYoUtS aT pHoToBlOg...".
def monthCheck(dateSep):
    if dateSep in months2:
        try:
            if dateSep == "STYCZNIA":
                month = "01"
            elif dateSep == "LUTEGO":
                month = "02"
            elif dateSep == "MARCA":
                month = "03"
            elif dateSep == "KWIETNIA":
                month = "04"
            elif dateSep == "MAJA":
                month = "05"
            elif dateSep == "CZERWCA":
                month = "06"
            elif dateSep == "LIPCA":
                month = "07"
            elif dateSep == "SIERPNIA":
                month = "08"
            elif dateSep == "WRZEśNIA":
                month = "09"
            elif dateSep == "PAźDZIERNIKA":
                month = "10"
            elif dateSep == "LISTOPADA":
                month = "11"
            elif dateSep == "GRUDNIA":
                month = "12"
            return month
        except:
            month = "00"
            return month
    elif dateSep in (months):
        try:
            if dateSep == "STY":
                month = "01"
            elif dateSep == "LUT":
                month = "02"
            elif dateSep == "MAR":
                month = "03"
            elif dateSep == "KWI":
                month = "04"
            elif dateSep == "MAJ":
                month = "05"
            elif dateSep == "CZE":
                month = "06"
            elif dateSep == "LIP":
                month = "07"
            elif dateSep == "SIE":
                month = "08"
            elif dateSep == "WRZ":
                month = "09"
            elif dateSep == "PAź":
                month = "10"
            elif dateSep == "LIS":
                month = "11"
            elif dateSep == "GRU":
                month = "12"
            return month
        except:
            month = "00"
            return month
# TEST = OK

# Gets post's title (for earliest post will be empty or fixed as "Photoblog <username> w Photoblog.pl")
def getTitle(soup):
    titleRAW = soup.find("meta", property="og:title")
    title = titleRAW.get("content", None)
    return title
# TEST = OK

# Fetches the note content.
def getNote(soup):
    try:
        noteRAW = soup.find("div", id="photo_note").contents
        # print(noteRAW)
        tmp = []
        for note in noteRAW:
            tmp.append(str(note))
        for row in tmp:
            tmp_row = row
            clean = re.compile('<.*?>')
            tmp_row = tmp_row.replace("</p>", " ")
            tmp_row = re.sub(clean, '', tmp_row)
            note = note + tmp_row
            # note = note.replace("\n", " ")
            # note = note.replace("\t", "")
            #note = " ".join(note.split())
            #note = " ".join(re.findall(r"[a-zA-Z0-9\.À-ž ]+", note))
        return note
    except:
        note = "Unable to fetch the note, unknown source format"
        print(note)
        return note
# TEST = OK\

# Fetches the next page of the user content.
def getNextPage(soup):
    try:
        nextPageRAW = soup.find("span", id="photo_nav")
        nextPage = nextPageRAW.find("a", string="poprzednie »").get("href")
        return nextPage
    except:
        nextPageRAW = soup.find("a", {"class": "prev"}, href=True, )
        nextPage = nextPageRAW.get("href")
        return nextPage
# TEST = OK

# Checks if the post is the last one
def checkIfLast(soup, isFirst):
    if isFirst:
        try:
            if getNextPage(soup).split("/")[4]:
                isLast = False
                return isLast
        except:
            isLast = True
            return isLast
    else:
        try:
            checkIfLastRAW = soup.find("span", id="photo_nav")
            list = []
            for a in checkIfLastRAW.find_all('a', href=True):
                list.append(a['href'])
            if len(list) == 1:
                isLast = True
            else:
                isLast = False
            return isLast
        except:
            if soup.find("a", {"class": "prev disabled"}, href=True, ):
                isLast = True
            else:
                isLast = False
            return isLast
# TEST = OK

# Fetches the number of post
def getPostnumber(soup):
    postNumber = getPhoto(soup).split("/")[5].split(".")[0]
    return postNumber
# TEST = OK

# the post desc (shorter version for post)
def getDescription(soup):
    descriptionRAW = soup.find("meta", property="og:description")
    description = descriptionRAW.get("content", None)
    return description
# TEST = OK

# Cooks a nicely parsed HTML soup for ye to be mined for sweets
def getSoup(fullURL):
    if statusCheck(fullURL):
        page = requests.get(fullURL)
        soup = BeautifulSoup(page.content, 'html.parser', from_encoding="iso-8859-8")
    else:
        print("process terminated")
        quit()
    return soup
# TEST = OK

# Just a precaution - verifies if the user has expired. You know. Just in case.
def checkIfExpired(soup):
    possibility = ["nie istnieje w serwisie Photoblog.pl", "nie dodał jeszcze żadnego wpisu"]
    try:
        expired = soup.find("div", {"class": "msgb_text"}).contents[3]
        expired = expired.decode().replace(".</p>", "").split("<br/>")
        if expired[1] in possibility:
            isexpired = True
        else:
            isexpired = False
    except:
        isexpired = False
    return isexpired
# TEST = OK

# Checks if Your photoblog is Password-protected. If it is - no scraping for ye, my friend. Turn off password for
# a while and then hit this the scrapping masterpiece.

def checkIfPasswordProtected(soup):
    try:
        psswd = soup.find("div", {"class": "show_midoptions_w"}).contents[1]
        psswd = psswd.decode().replace("<h3>", "")
        psswd = psswd.replace("</h3>", "")
        if psswd == "Ten fotoblog zabezpieczony jest hasłem.":
            isProtected = True
        else:
            isProtected = False
    except:
        isProtected = False
    return isProtected
# TEST = OK

############## CORE ##############
print("################# INIT INFO #################")
print('\n\nI Hereby humbly inform You, that the scraping process of Your public photoblog account commences!')
print('\nLike...')
print('\n\n\t\t\tNOW!\n\n')

print(
    "I'm scrapping photoblog account:", URL_userName, "\nStarting at:", datetime.datetime.now(),
    "\nThe files will be dropped to: \nIMAGES:\t", filesdrop_image, "\nPOST:\t", filesdrop_story,
    "\n\nHOPE YOU'LL ENJOY MY WORK AS I AM LIKE THE BEST SCRIPT EVER! CHEERS!"
)

print("################# DIR CHECK #################")
print("NOW I'M CHECKING IF THE DROP DIRECTORY EXISTS.")
print("YOU KNOW... TO PUT ALL THAT USELESS JUNG FROM YOUR ACCOUNT")
print("NOTHING TO SEE HERE...\n\n")
# CREATE LOCATIONS IF NOT EXISTENT

if os.path.isdir(filesDrop_main) == True:
    print("Directory", filesDrop_main, "exists")
else:
    os.makedirs(filesDrop_main)
    print('Directory', filesDrop_main, "created")
if os.path.isdir(filesdrop_image) == True:
    print("Directory", filesdrop_image, "exists")
else:
    os.makedirs(filesdrop_image)
    print('Directory', filesdrop_image, "created")
if os.path.isdir(filesdrop_story) == True:
    print("Directory", filesdrop_story, "exists")
else:
    os.makedirs(filesdrop_story)
    print('Directory', filesdrop_story, "created")

print("\n\n################# NOW REAL WORK BEGIN #################")
print("\n\t\t\tMUAHAHAHAHAHAHAHAH")

isFirst = True
isLast = False
listofscrapedphotos = os.listdir(filesdrop_image)
listofscrapedstories = os.listdir(filesdrop_story)
print("photos already in place:", listofscrapedphotos)
print("posts already in place:", listofscrapedstories)
soup=getSoup(fullURL)
if not checkIfPasswordProtected(soup):
    if not checkIfExpired(soup):
        if not checkIfLast(soup, isFirst):
            while not isLast:
                if not checkIfLast(soup, isFirst):
                    downloadPhoto(soup, filesdrop_image, listofscrapedphotos)
                    downloadPost(soup, listofscrapedstories)
                    URL_postNumber = getNextPage(soup).split("/")[4]
                    fullURL = URL_base + "/" + URL_userName + "/" + URL_postNumber
                    if statusCheck(fullURL) == True:
                        page = requests.get(fullURL)
                        soup = BeautifulSoup(page.content, 'html.parser')
                    else:
                        print("process terminated")
                        quit()
                    isFirst = False
                else:
                    downloadPhoto(soup, filesdrop_image, listofscrapedphotos)
                    downloadPost(soup, listofscrapedstories)
                    isLast = True
