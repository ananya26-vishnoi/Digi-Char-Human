# Digi-Char-Human

Digi-Char-Human is a project which aims to automatically generate <b>whole body pose animation + facial animation</b> on 3D Character models based on the camera input.
<br/>




## About Digi-Char-Human 
Digi-Char-Human  is a system for bringing automation in animation generation on 3D virtual characters.
It uses Pose estimation and facial landmark generator models to create entire body and face animation on 3D virtual characters.
<br/>
Digi-Char-Human  is developed with [**MediaPipe**](https://github.com/google/mediapipe) and **Unity3D**.
MediaPipe generates 3D landmarks for the human whole body and face, and Unity3D is used to render the final animation after processing the generated landmarks from MediaPipe. 




<!-- GETTING STARTED -->
## Installation
Follow the instructions to run the program!
### Backend server installtion
1. Install MediaPipe python.
  ```py
   pip install mediapipe
   ```
3. Install OpenCV python.
  ```py
   pip install opencv-python
   ```
5. Go to `backend` directory and install other requirements:
  ```py
   pip install -r requirements.txt
   ```
6. You'll need to [download](https://drive.google.com/file/d/15VSa2m2F6Ch0NpewDR7mkKAcXlMgDi5F/view?usp=sharing) the pre-trained generator model for the COCO dataset and place it into `backend/checkpoints/coco_pretrained/`.

### Unity3D Installation
Install Unity3D and its requirements by the following guidelines(Skip 1-3 if Unity3D is already installed).
1. Download and install  [UnityHub](https://unity.com/download)
2. Add a new license in UnityHub and register it
3. Install a Unity Editor inside UnityHub(`LTS` versions and a version higher than `2020.3.25f1` are recommended).
4. In the Unity project setting, allow HTTP connections in the player setting.
5. Download and import the following packages into your project to enable the recording option available with FFmpeg(Download `.unitypackage` files and drag them to your project).

# Usage
- Run backend server at `backend` directory with the following command:
  ```
   python server.py
   ```
- Run Unity Project and open the main scene at `Assets\Scenes\MainScene.unity`
- Test the program by uploading videos to backend from the Unity project(You can test the application by selecting provided animations from the right side menu!).

## Adding new 3D characters
You can add your characters to the project!
Characters should have a standard Humanoid rig to show kinematic animations. For rendering face animations, characters should have a facial rig(Blendmesh).</br>
Follow these steps to add your character:
1. Find a 3D character model from [Unity asset store](http://assetstore.unity.com/) or download a free one(You can download them from websites like [Mixamo](http://mixamo.com/)).
2. Open the character setting and set the rig to humanoid
3. Drag and drop your 3D character model to `CharacterChooser/CharacterSlideshow/Parent` object in Unity main Scene like the image below
4. Add `BlendShapeController` and `QualityData` components to the character object in the scene(which is dragged inside the Parent object in the last step).
5. Set `BlendShapeController` values
- Add character `SkinnedMeshRenderer` component to `BlendShapeController` component.
- Find each blnedShape weight number under `SkinnedMeshRenderer` and set those numbers in `BlendShapes` field inside `BlendShapeController` (for specifying each blendshape value to the `BlendShapeController` component so the animation would be shown on character face by modification on these blnedShape values)
6. Open `CharacterSlideshow` Object on `CharacterChooser/CharacterSlideshow` path inside the scene hierarchy, then add a new dragged character to the `nodes` property(all characters should be referenced inside `nodes`).
7. Run the application and you can now select your character for rendering animation!

# Features
<!-- ROADMAP -->

<!-- ## Available features -->
- [x] Making full body animation
- [x] Animating multiple blendShapes on 3D character (up to 40 blendshape animations is supported currently)
- [x] Supporting any 3D models with Humanoid T-Pose rig
- [x] Exporting animation in a video file
- [x] Saving animation data and re-rendering it for future usage
- [x] Filtering mediaPipe outputs in order to detect and remove noises and better smoothness (Low Pass Filtering is used currently) 

<!-- ## TODO -->

- [ ] Animating the character's face in great details
    - [ ] Training a regression model to generate Blendmesh weights by feeding the output data of mediaPipe FaceMesh(468 points)
    - [ ] Using StyleGan techniques to replace whole character face mesh
- [ ] Automatic rigging for 3D models without humanoid rig (Using deep neural network models like RigNet)
- [ ] Generating complete character mesh automatically using models like PIFuHD (in progress!)
- [ ] Animating 3D character mouth in great detail using audio signal or natural language processing methods
- [ ] Generating complete environment in 3D