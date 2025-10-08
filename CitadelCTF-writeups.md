# CITEDAL CTF WRITEUPS
This is just a heads-up. I don't have a great experience of solving CTFs prior to this CTF and that too in a team environment. So, I was able to solve the easier ones (the 100 points challenges), but I took help from my teammates to solve the rest of the challenges (the 200 points one). 

# 1. Zahard's Welcome

## My solution
**Flag:** `citadel{7h3_c174d3l_b3ck0n5}`

## LOGIC
1. I felt, as any other ctf, this was just a start into ctf challenges. What we need to do was just join the discord server -  https://discord.gg/FfBw8VzfRR and search for the flag. 
2. Usually, when we join a server, we look through the different channels, especially, we would run through the rules. That is, what my team did as well and we found the flag amongst the rules .

# 2. The Social Network

## My solution
**Flag:** `citadel{17_1s_jus7_7h3_b3g1nn1ng}`

## LOGIC
1. In the question its said : Start by checking out citadweller on Instagram. So, we did the same and found the first part of the flag `citadel{17_1s_`
2. It was also given, to follow the X account. And the bio of the X account had the 2nd part : jus7_7h3_b3g1nn1ng} .

# 3. Omniscient Flag's Metadata

## My solution
**Flag:** `citadel{th1s_ch4ll3ng3_1s_f0r_th4t_0n3_ex1ft00l_4nd_b1nw4lk_enthus14st}`

## LOGIC
1. The challenge gave us a jpeg file. And from the title of the challenge, it is hinted that this challenge has something to do with the metadata of the image file.
2. So, we upload the image file in a metadata website : https://www.metadata2go.com/ 
3. In the metadata list, at the author section, it gave : kdj had a habit of hiding images within images.
4. From this we understood that the image file has another image inside it.
5. So, Inorder to extract the hidden image file, we ran the jpeg file through a ONLINE BINWALK UTILITY website, which gave the png file, which had the flag!!


# 4. Track 8

## My solution
**Flag:** `citadel{add_vinegar_twice}`

## LOGIC
1. In the question, it is referencing the word 'CIPHER', which made me guess that its gonna be something related to cipher only
2. According to what I have seen, most of the cipher text are Vigenere Cipher
3. Also, we need a key for decoding this text. By reading the question and from the title, we can identify it referencing to some music context and the question also references 'Panchiko's album', so one of our guess was the word : 'panchiko' as the key.
4. On solving, the above, we got the flag.

# 5. Test of Sweetness

## My solution
**Flag:** `citadel{fru1tc4k3_4nd_c00k13s}`

## LOGIC
1. This question is an easy web challenge. On clicking the link given in the question, we are directed to a website that has the message : "ONLY ADMINS CAN GET THE SECRET MESSAGE". 
2. In every web challenge, you inspect the website. On doing so and entering the cookie directory, where a cookie called user with a value as user exists.
3. In order to become admin, we just change the value of user to admin and then, refresh the page, which reveals the flag on the main page.

# 6. Selected Ambient Work

## My solution
**Flag:** `citadel{1_L0V3_1DM}`

## LOGIC
1. From the audio file given in the question, playing it for a few seconds, we find out that the audio given is morse code, which we need to decode.
2. But the problem was that, there was a background music playing along with it, so it was quite hard to detect it through a normal morse code decoder. 
3. Then, we came across an idea that, why not try filter out the frequency, ie concentrate the frequency at a particular point, which resonates with the morse code, thus filtering out the background music and thus, we are able to decode the morse code.
4. So, we found a website 'Morse Code Sound & Vibration Listener` ( link given in references ), where we are able to set the frequency at a particular point as well as decoding the morse code at the same time.
5. We uploaded the audio file and made trial and error methods to try and figure out the frequency where morse code is being detected. We found out that it was getting detected at around 750 Hz, as shown in the figure 
<img width="1312" height="866" alt="citedal" src="https://github.com/user-attachments/assets/11a1829a-e73b-4d9a-8044-7e5e47ed3d7a" />

6. As the citadel{ } bracket opened and closed, the morse code between that time frame was taken as the flag's value and which is the actual flag!!

## References 
1. https://databorder.com/transfer/morse-sound-receiver/ - For decoding the morse code

# 7. schlagenheim

## My solution
**Flag:** `citadel{8lackM1D1wa5c00l}`

## LOGIC 
1. When you check the given file, it has a .wav extension, which usually means it’s an audio file. But when you open it in a hex editor to see its raw bytes, you notice something unusual, that the file starts with the letters M1D1 instead of the normal “RIFF” header that a .wav file should have. This is a strong hint that the file is not really a WAV, but actually a MIDI file.
2. The clue also matches the challenge name and description.
3. To fix this, you need to change the header of the file. Replace the M1D1 in the beginning with MThd, which is the correct magic bytes for a MIDI file. These bytes tell the computer that the file is indeed a MIDI format. 
( It is my teammates who did these steps and I did the upcoming steps )
4. After making this small edit, save the file with a .mid extension instead of .wav. 
5. Now, I opened FL Studio and opened the new MIDI file in it, in the Piano Roll, where the notes became letters or words.
6. And these notes revealed the flag!!
![CTF](https://github.com/user-attachments/assets/f854e825-b9e0-4daa-9277-e456ce401fc5)




