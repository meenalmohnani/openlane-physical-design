# openlane-physical-design

## Day 3 lab

Cloning github project
![image](https://user-images.githubusercontent.com/71206467/183241804-624b4299-879f-408b-b751-c098200a4c5d.png)

We will perform spice extraction and post layout

![image](https://user-images.githubusercontent.com/71206467/183242463-1662e1fe-38f4-4d84-9e82-b70ff34bd9b3.png)

Invertor in magic
red is polysilicon , when you hover on the colour pallet, the name of the layer is shown
![image](https://user-images.githubusercontent.com/71206467/183249401-3e38ffee-6bcf-4501-97de-a84d9a8aebb2.png)

![image](https://user-images.githubusercontent.com/71206467/183251300-fb521adc-9b0f-4247-8cfc-c0ef8d88f965.png)
The highlighted portion is a nmos

![image](https://user-images.githubusercontent.com/71206467/183251338-39d52bb5-2f98-4b5a-aa9c-7d8794e485bf.png)

The highlighted portion is a pmos

![image](https://user-images.githubusercontent.com/71206467/183259713-52fe96d0-a0b3-43af-b113-8856f75aaa9d.png)

The command to extract the netlist

![image](https://user-images.githubusercontent.com/71206467/183259878-4a74ff6c-8012-4ceb-92d1-7072fc35e89b.png)
The command to create spice file


![image](https://user-images.githubusercontent.com/71206467/183259922-605ae2d6-6eea-44ad-9aed-6d2a0cef36a1.png)
Spice file created

![image](https://user-images.githubusercontent.com/71206467/183261496-414df4ef-767a-49bf-b9f9-76dd9b1e0c02.png)
changing scale and adding pshort and nshort files


![image](https://user-images.githubusercontent.com/71206467/183284514-e39607e1-6898-40be-80d1-3b293a617807.png)
Editing the spice file

![image](https://user-images.githubusercontent.com/71206467/183284669-454a2ae5-b81a-4761-a940-77017c313ac0.png)
Ploting input and output in spice file

![image](https://user-images.githubusercontent.com/71206467/183285079-77b843f5-d740-492a-a2c8-b1439440da27.png)
values of 20% of the maximum and 80% of the maximum

difference 0.0636 ns

## Day 4

From PnR point of view you need to follow some certain guidelines while making the standard cell set
1) The input and the output port must lie on the intersection of vertical and horizontal tracks
2) The width of the standard cell should be odd multiple of the track pitch
3) The height should be odd multiple of the track vertical pitch

Tracks are basically used at the routing stage
![image](https://user-images.githubusercontent.com/71206467/183287038-7c543e77-6de4-42c5-be32-c42a14eb5a94.png)


Tracks store the information on which metal layer the routing is done
offset and pitch are given in the image

![image](https://user-images.githubusercontent.com/71206467/183304442-65055060-7b8c-4814-81fc-f228120e5bf6.png)

![image](https://user-images.githubusercontent.com/71206467/183304541-93950908-6a8c-43bf-baae-43bc5228768c.png)
It has removed the existing run

![image](https://user-images.githubusercontent.com/71206467/183305693-ec0232c3-f61f-41fd-a1b5-789720bce3ef.png)

Merging our custom inverter lef to the design
These three steps were to ensure that merged.lef gets created

![image](https://user-images.githubusercontent.com/71206467/183305813-d76527e4-9bb9-4d43-9b0b-c9a08407ce61.png)

After running the synthesis showing tns = 711 and wns = 23.89

![image](https://user-images.githubusercontent.com/71206467/183305893-7b90b086-9727-4c3e-b591-1a26f5a4c484.png)

statics report showing the area used

![image](https://user-images.githubusercontent.com/71206467/183305980-65bd9052-2932-44de-8496-7a2275b89def.png)

timing report containing the worst negative slack

![image](https://user-images.githubusercontent.com/71206467/183306071-311a3629-b316-46b5-9c64-e0b8a90ff03a.png)
 
 Opening readme file to check parameters which we will change for optimising timing 
 
 ![image](https://user-images.githubusercontent.com/71206467/183306589-4920dee3-e985-40b0-a645-643e45ce5f1d.png)

Checking and setting the synthesis paramenters in command promt

both pmos and nmos are slow slow type means they will have max delay
synthesis buffering : you want high fanout pins to be buffered , this in a way reduces the wire delay 

inv 8 has a good drive strength

![image](https://user-images.githubusercontent.com/71206467/183359589-216bbbc3-cff7-40ab-9018-4345c69aee22.png)

setting synthesis strategy to delay 1

![image](https://user-images.githubusercontent.com/71206467/183361144-098bdb0e-a864-4450-ba84-d96a963c05c8.png)

running synthesis after changing parameters
negative slack got 0 means no violation

![image](https://user-images.githubusercontent.com/71206467/183362911-c7126699-8e6d-4795-8540-ba0e01b0e006.png)

Our custom standard cell is present in the merged.lef

![image](https://user-images.githubusercontent.com/71206467/183364636-0c78f261-c615-4851-982d-f8bb95553b86.png)

running floorplan using init_floorplan command

![image](https://user-images.githubusercontent.com/71206467/183365299-5c209697-8f16-4178-b84f-8e47060301e9.png)

placing i/o

![image](https://user-images.githubusercontent.com/71206467/183365827-86cfd4b1-3185-4285-b703-2927b7d578e9.png)

No slack found after running gloabal placement

running detailed routing
inserting taps

![image](https://user-images.githubusercontent.com/71206467/183365993-f8fb60ae-ccc9-4dd6-8891-b255bbb10c98.png)

![image](https://user-images.githubusercontent.com/71206467/183368517-ade7644c-c7af-44e7-9879-aefca61fd33e.png)

![image](https://user-images.githubusercontent.com/71206467/183368091-ef899c49-3855-4947-bea4-91efcdeb2dfb.png)


opening placement in magic

![image](https://user-images.githubusercontent.com/71206467/183369713-3ff08dd4-e4c2-45c5-b5e5-0fbb5b0f2f14.png)
vsd inv cell in the design 
overlapping means sharing of vdd and gnd

![image](https://user-images.githubusercontent.com/71206467/183391342-98837c22-5e77-43b0-a0bd-b5b4fe81ac99.png)
fast.lib is for hold analysis

![image](https://user-images.githubusercontent.com/71206467/183392171-4fd3f4f4-1b7e-4f0f-aa59-91a63ede94b6.png)


slack after running sta analysis

![image](https://user-images.githubusercontent.com/71206467/183395815-cb9cc2a4-b4e2-42ad-8785-20b23e64bb87.png)

changing max fanout and running synthesis again

decreasing fanout increased the tns in my case

![image](https://user-images.githubusercontent.com/71206467/183412466-ab597ac0-b5dc-4f1c-b870-d9c40c40b33d.png)

total 161 driver pins for this net

![image](https://user-images.githubusercontent.com/71206467/183421772-a0d12e06-9d82-45ae-af6b-605c0924a2db.png)

After running CTS

![image](https://user-images.githubusercontent.com/71206467/183429481-7125fcf3-0c9e-48d7-83b3-c30f23e9e730.png)
invoking openroad

![image](https://user-images.githubusercontent.com/71206467/183436220-8a9a6b28-d54d-4767-9cde-73409adf8257.png)

slack violated

After running the correct analysis slack is met
![image](https://user-images.githubusercontent.com/71206467/183440371-8fe921bd-d817-4224-8f7b-96c38d0daab9.png)



## Day 5

![image](https://user-images.githubusercontent.com/71206467/183460030-39c79adc-9f09-461a-a8e5-85420eb0bddf.png)

running power distribution network

![image](https://user-images.githubusercontent.com/71206467/183462307-ce9d93cf-0e3a-49e9-acda-15ff9646194a.png)

Standard cell rail info

 ![image](https://user-images.githubusercontent.com/71206467/183464098-4a1ba733-324b-4fea-b138-71721379980b.png)

Green box is picorv 
Yellow boxes are io pads 
Blue is ground and red is power pad
From the pad the power gets supplied to the ring and from the ring to the straps and from the straps it is going to the standard rails
Square at the corner are corner pad

![image](https://user-images.githubusercontent.com/71206467/183464829-4c003834-6119-428c-b2bd-30d86ef0f11c.png)

Running routing

![image](https://user-images.githubusercontent.com/71206467/183472096-4e53203d-c2dc-4e81-94ae-77b5ee4d5859.png)
After 57th optimization the no. of violations are 0

![image](https://user-images.githubusercontent.com/71206467/183472747-e427da87-15b2-4272-967d-6a4363c7c463.png)

DRC file is empty ,no violations are there








