

# Task 1

The encryption key is `bhUlIshutrea98liOp` as it's loaded before going to the encrypting part of the ransomware. 
 
![Screenshot 2025-02-23 153042](https://github.com/user-attachments/assets/710d4d29-1840-4fb0-8e85-045803f013b8)


# Task 2

After knowing the encryption key, I have to know the encryption algorithm used to encrypt files. I opened the ransomware file using Ghidra. There is a function which is called `encrypt_file` and after analyzing it statically, I found that it uses XOR encryption algorithm. The following pseudocode shows the the for loop used for encrypting files. 

![Screenshot 2025-02-26 132151](https://github.com/user-attachments/assets/16a314f6-a07d-452d-9d19-cb40250d07c3)


The red rectangle is the for loop and the yellow one is code that encrypts each element in the file with the corresponding character in the encryption key. `param_2` is the encryption key and `bVar1` is the element in the file that will be encrypted. 

I used ChatGPT to write the decryption code of this encryption algorithm in python and the output is: 
```python

def xor_decrypt(file_path, key, output_path):
    try:
        # Read the encrypted file as binary
        with open(file_path, 'rb') as encrypted_file:
            encrypted_data = encrypted_file.read()

        # Repeat the key to match the length of the data
        key_bytes = bytearray(key, 'utf-8')
        key_length = len(key_bytes)
        decrypted_data = bytearray(len(encrypted_data))

        # Perform XOR decryption
        for i in range(len(encrypted_data)):
            decrypted_data[i] = encrypted_data[i] ^ key_bytes[i % key_length]

        # Write the decrypted data to the output file
        with open(output_path, 'wb') as output_file:
            output_file.write(decrypted_data)

        print(f"Decryption complete. Decrypted file saved at: {output_path}")

    except FileNotFoundError:
        print("Error: The input file was not found.")
    except Exception as e:
        print(f"An error occurred: {e}")

# Example usage:
encrypted_file_path = "/home/kali/Desktop/lockpick1/forela-criticaldata/trading-firebase_bkup.json.24bes"  # Path to the encrypted file
decryption_key = "bhUlIshutrea98liOp"          # The XOR key used for encryption
output_file_path = "/home/kali/Desktop/lockpick1/forela-criticaldata/trading-firebase_bkup.json"     # Path to save the decrypted file

xor_decrypt(encrypted_file_path, decryption_key, output_file_path)

```

The code explains itself using the written comments. I decrypted each file in the `forela-criticaldata` folder and storing the decrypted data in a file which has the original file name without the file extension `.24bes`. These are the files after decrypting them: 

![Screenshot 2025-02-26 133412](https://github.com/user-attachments/assets/46ffec63-0895-4731-9ede-588eba0112ef)


In this task, it says that the email address `wbevansn1@cocolog-nifty.com` has made a mistake in the application process so I searched in `forela_uk_applicants.sql` file for this email address and I found these first name `Walden` and second name `Bevans` as illustrated in the following image: 

![Screenshot 2025-02-26 133739](https://github.com/user-attachments/assets/6f8aa553-78f7-4051-8199-44f451751384)


# Task 3

In order to get the MAC address and the serial number of  the laptop assigned to `Hart Manifould`, I opened `it_assets.xml` file and searched for that name andthe result is: 

![Screenshot 2025-02-26 134101](https://github.com/user-attachments/assets/24c05280-8ea9-4012-9274-bca616885893)



# Task 4

The email address of the attacker is found as `bes24@protonmail.com` like the following image: 

![Screenshot 2025-02-26 140135](https://github.com/user-attachments/assets/5783ca97-0ea4-4480-a6fa-9a6035c091eb)


# Task 5

I need to search for someone in the `trading-firebase_bkup.json` file who has the greatest profit percentage so I used this command `grep -o '"profit_percentage":[ ]*[0-9]\+[.]\?[0-9]*' trading-firase_bkup.json | sed 's/"profit_percentage"://g' | sort -g | tail -1` to filter the search findings and the explanation of this line is:
1. `grep -o '"profit_percentage":[0-9.]\+' trading-firebase_bkup.json`:
    - Extracts all occurrences of numbers after `"profit_percentage":`.
    - Matches both integers and decimal numbers.
2. `sed 's/"profit_percentage"://g'`:
    - Removes the `"profit_percentage":` prefix, leaving only the number.
3. `sort -g`:
    - Sorts the numbers according to general numerical value.
4. `tail -1`:
    - Displays the highest number.

In the following image, the number `142303.1996053929628411706675436` is the greatest profit number in the file.

![Screenshot 2025-02-26 150236](https://github.com/user-attachments/assets/8a55d249-febc-4ca4-a66f-fa95de920157)


After that, I search for the email address using this number and the email address is `fmosedale17a@bizjournals.com` as illustrad in the following screenshot:

![Screenshot 2025-02-26 150925](https://github.com/user-attachments/assets/89520b0b-3eaf-4777-859b-b59354f265ef)



# Task 6

The task asks for the IP address of `Karylin O'Hederscoll` in `Sales Forecast` log file so I search for that name and I found the IP address is `8.254.104.208` as shown in the following image:

![Screenshot 2025-02-26 151415](https://github.com/user-attachments/assets/95c414b3-d25d-4bc1-ba36-c2264419dc9d)


# Task 7

After I extracted the file extensions from the file using the following command `strings bescrypt3.2 | grep .`, these are the targeted file extensions:

![Screenshot 2025-02-26 170806](https://github.com/user-attachments/assets/f7a9c3b3-49da-4a29-bbf2-35180da0a825)

So the answer is `.ppt`.


# Task 8

Calculating the MD5 hash of the applicants DB:

![Screenshot 2025-02-26 171404](https://github.com/user-attachments/assets/348d2861-fe1c-42de-9902-deb2766fa74f)


# Task 9 

Calculating the MD5 hash of the trading backup:

![Screenshot 2025-02-26 171618](https://github.com/user-attachments/assets/db0a09cf-e897-43d9-9781-8f1646ddc417)


# Task 10 

Calculating the MD5 hash of the complaints file:

![Screenshot 2025-02-26 171952](https://github.com/user-attachments/assets/d9eff7b1-4ccf-4b01-a12f-f3499751fd27)
