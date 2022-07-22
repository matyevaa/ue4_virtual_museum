# Immersive & Interactive Contemporary Art Museum

For people of all ages and backgrounds who are interested in exploring things, the proposed immersive contemporary art museum would be a great experience that allows everyone to explore virtual reality and examine the compositions of contemporary art from professional, amateur, or any other point of view.

Unlike most of the VR applications that involve solving logical problems, overcoming challenges, fighting, or shooting that may not be suitable for everyone, the museum would offer the audience to peacefully explore the variety of one-of-a-kind art compositions in a user-friendly, static VR environment suitable for people of all ages and backgrounds.

## Topic Selection

Contemporary art is a broad genre, thus the project was narrowed to focus mostly on contemporary surrealism. 

With the creativity freedom in styling and setting up the props, the museum got an emphasis on magic and strange beauty in the unexpected things.
A variety of random stuff was use to create bright, unique, and creative compositions that can surprise everyone and make our museum special, interesting, and worth exploring.

The props were set up around the museum in individual art compositions. Users would be able not just to explore the art visually, but also experience interactivity by pressing buttons and seeing how art compositions change in unique ways.

## Plan

![image](https://user-images.githubusercontent.com/59642740/180339110-ef320864-3f36-4516-9e61-a7bc494d1cd8.png)

## Research

![research](https://user-images.githubusercontent.com/59642740/180339671-da0a86ad-fa34-463c-99c7-7e8564dc5976.png)

## Art Compositions
![art](https://user-images.githubusercontent.com/59642740/180339686-4037b5f1-5053-4585-a9ae-65e6c4d9a540.png)
![art 2](https://user-images.githubusercontent.com/59642740/180339689-5ee14dbb-efbe-4e65-88c3-eac9c2204903.png)

## Rooms

![entranc](https://user-images.githubusercontent.com/59642740/180339696-a49037dd-b820-40b9-96a5-d379f18d0bb8.png)
![display](https://user-images.githubusercontent.com/59642740/180339703-99cf4878-792e-4e7d-b9a1-fd978e0e8749.png)
![sculture](https://user-images.githubusercontent.com/59642740/180339709-3b05471a-f82f-483e-a9bf-6e1ccdfe7f0c.png)

## UE4 Blueprints Documentation

The main blueprints that were used for the creation of the museum project include the user's interaction with the button. To increase the user’s experience within the small development time given, the button’s blueprint was repurposed into multiple different interactions. A single algorithm was implemented for three buttons that can execute the following operations after being toggled (see Figure 1), depending on the button’s location:

* Changing lights status around the museum environment;
* Changing the video player status in one of the museum rooms;
* Changing the location of the mesh components in the museum kitchen art composition. 

![1](https://user-images.githubusercontent.com/59642740/180338812-9b43fa85-6c6c-48ef-9d1d-34153f525d4b.png)

Changing lights status around the museum environment starts with the user’s interaction with the button at the main entrance of the museum. After the button is pressed, the system checks whether the lights are on by setting a branch condition on actor lights status. If true, it changes the lights status to the opposite (off), else - the lights are changed to be on. In direct relation to the lights' status, the change in paintings switches from on and off respectively. See Figure 2 for the visual diagram of how the lights blueprint workflow goes.

![2](https://user-images.githubusercontent.com/59642740/180338826-3114eceb-6ddf-4fa9-9673-1d7c4d56a2ec.png)

A tag is assigned to each of the light actors (spotlights) that are then pushed into a single array. After the button is pressed, the Toggle Lights function is executed, where each element of the lights array goes through the loop. It checks the status of light with the branch condition and changes it to the opposite. If lights are determined to be on, their visibility is set to hidden. See Figure 3 for the toggle lights operation workflow.

![3](https://user-images.githubusercontent.com/59642740/180338843-68038790-fa88-4caf-8378-d5e496b6ff16.png)

Change in paintings occurs after the lights button is toggled by the VRpawn actor reference that is tracking the interaction of the user with the specific button LightsButton: from each element in the lights array, the boolean lightStatus is determined and passed to the ToggleLights to switch the lights status from on and off respectively. Depending on the lightStatus, ChangePaintings gets the opposite value of the lightStatus, making ChangePaintings true if the lights are off and false if they are on. 

In a similar manner to the lights array mentioned before, another tag is assigned to the paintings actor components, which are then pushed into one array. This way, all the paintings with the paintings tag are iterated one by one within one array with their emissive property toggled in accordance to the lightStatus boolean value. See Figure 4 for the Change Paintings function workflow.

![4](https://user-images.githubusercontent.com/59642740/180338857-5f1cb41e-4fd6-455b-8457-a9d422634fe2.png)

Similarly to the interaction with the LightsButton, the user can press the button in the kitchen. After the button is pressed, the branch condition evaluates the status of the furniture by checking if it has been moved or not. The furniture actor components are tagged as kitchenProp and put into one array. If the branch condition’s output is false, the elements from the kitchenProp array are iterated one by one within the loop, and the z axis coordinate of each kitchenProp element is compared to the hardcoded height float value with the branch condition. If the height of the element is smaller, the objects are animated up. Else, when the kitchenProp element height is bigger than zero, the objects are animated down. See Figure 5 for the kitchen furniture composition functionality workflow.

![5](https://user-images.githubusercontent.com/59642740/180338871-1a2cd48c-59d2-488c-a2aa-338b5099679d.png)

The user can press the button to play video on the wall as well. The passed parameters include the video content, which is the media reference of the media player, and the video’s audio, which is the indicated sound wave. After the button is pressed, the media player’s playing status is evaluated with the branch condition. If true, the video and audio are paused, else - they are played. Refer to Figure 6 for the video player’s functionality workflow.

![6](https://user-images.githubusercontent.com/59642740/180338885-2228e37a-37f0-4443-984f-a060160bd021.png)

