port os, random, string, sys
print ("welcome to the password generate and checker")

##my_symbols = "!" ,"$" ,"%" ,"^" ,"&" ,"*" ,"(" ,")" ,"-" ,"_" ,"=" ,"+"]
my_symbols = "!$%^&*()-_=+"
not_allowed_symbols = ["@" ,"£" ,"<" ,">" ,"?" ,"/" ,"§" ,"±" ,"{" ,"}" , "[" ,"]" , "." ,"," ,":" ,";" ,"|" ,"#" ,"€"]

def check_password(passwordcheck):
##    passwordcheck = input("Enter a password to check: ")
    checking=set(passwordcheck)
    passwordlength = len(passwordcheck)
    print ("your password is {} characters long".format(passwordlength))
    points = len(passwordcheck)

    qwerty = ["qwe","wer","ert","rty","tyu","yui","uio","iop","asd","sdf","dfg","fgh","ghj","hjk","jkl","zxc","xcv","cvb","vbn","bnm",
              "QWE","WER","ERT","RTY","TYU","YUI","UIO","IOP","ASD","SDF","DFG","FGH","GHJ","HJK","JKL","ZXC","XCV","CVB","VBN","BNM"]
#what querty is so if in password it will be caught 
    for a in not_allowed_symbols:
        if a in passwordcheck:
            print ("not a suitable character, please try again!")
            print ("Returning to main menu !")
            main_menu()
            
    if passwordlength <8 or passwordlength >24:
            print("error. the Password must be between 8-24 characters long or it can't be your password as it's not suitable")
            print ("Returning to main menu !")    
    else:

        for x in qwerty:

            if x in passwordcheck:  #If entered password is in the form of 'qwerty': system will subtract 15 points.
                points-=15
                print("your password contains a form of '3 consecutive letters  -15 points")
            
    if any(x.islower() for x in checking) or any(x.isupper() for x in checking) or any(x for x in checking if x in symbols) or any(x.isdigit() for x in checking):
        points +=5  #If there is at least one 'capital', 'lower case', 'symbol' or 'number': add 5 points.

    if any(x.islower() for x in checking) and any(x.isupper() for x in checking) and any(x.isdigit() for x in checking):
        points +=15 #If there is a capital and a number and a lower: add 15 points.
        
    if points <= 0:
        print("Weak Password !!  Points = {}".format(points))
        print("Returning to main menu")
        main_menu()#calling the main_menu method , to rerun it 
        
    elif points > 0 and points < 20:
        print("Medium Password !!  Points = {}".format(points))#.format will substitute the argument given , in to the {} braces
        print("Returning to main menu")
        main_menu()
        
    elif points  > 20:
        print("Strong Password !!   Points = {}".format(points))
        print("Returning to main menu")
        main_menu()

def get_random_string(min_chars=8, max_chars=24):
    all_chars = string.ascii_letters + string.digits + my_symbols
    random_str = "".join(random.choice(all_chars)
                         for _ in range(random.randint(min_chars, max_chars)))
    return random_str

def main_menu():
    menu= ()
    menu= int(input("[1]Quit     [2]Generate passsord     [3]Check password  : "))
    
    if menu == 1:
         print ("you have selected quit,goodbye")
         exit()
     
    elif menu == 2:
         random_password = get_random_string()
         print (random_password)
         print('Your password is:', random_password)
         passwordcheck = random_password
         check_password(passwordcheck)
         exit()

    elif menu == 3:
        print ("you have chosen option 3")
        passwordcheck = input("Enter a password to check: ")
        check_password(passwordcheck)
        exit()
        
    elif menu != 1 or 2 or 3:
        print ("You have chosen an incorrect option")
        main_menu()
              
main_menu()

##menu = main_menu


    
