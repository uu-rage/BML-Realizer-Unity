
# Table of Contents
- [BML Schema] (#bml-schema)
- [Unity3D Implementation] (#unity3d-implementation)

### BML Schema

In out example, we are using this BML schema

		<xml>
			<bml id="bml1" characterId="Sara">

			<speech id="speech1" start="0">
			  <text>Hello, my name is Sara.</text>
			</speech>
			
			<gesture id="gesture1" lexeme="gesture" start="0"/>

			<gaze id="gaze1" target="Cube" start="4" end="6"/>
				<gaze id="gaze2" target="Sphere" start="gaze1:end+1" end="gaze2:start+3"/>		
				<gaze id="gaze3" target="Capsule" start="gaze2:end+1" end="gaze3:start+3"/>		
				
				<speech id="speech2" start="gaze1:start+1">
					<text>I can look at cube</text>
				</speech>

			<speech id="speech3" start="gaze2:start+1">
			  <text>green sphere</text>
			</speech>

			<speech id="speech4" start="gaze3:start+1">
			  <text>or a blue capsule</text>
			</speech>

		  </bml>
		</xml>


### Unity3D Implementation

You need to define the package 

		using AssetPackage;
		using BMLNet;

Inside your class, you need to create variable for RageBMLNet

		RageBMLNet bml = new RageBMLNet();

To parse BML schema from file text

		bml.ParseFromFile("assets/BML.xml");
		
To parse BML schema from string 

        bml.ParseFromString(System.IO.File.ReadAllText("assets/BML.xml"));

Call Update eachtime Unity update the frame
		
		void Update () {
			// for every update, need to update BMLNet
			bml.Update(Time.deltaTime);
		}
		
In order to monitor the BML synchronization time, we need to assign the callback

        bml.OnSyncPointCompleted += SyncPointCompleted;
		
And this is the callback for synchronization

		void SyncPointCompleted(string behaviorID, string eventName)
		{
			BMLBlock block = bml.GetBehaviorFromId(behaviorID);
		
			GameObject character = GameObject.Find(block.getCharacterId());
			 if (block is BMLFace)
			{
				BMLFace face = (BMLFace)block;

			}
			else if (block is BMLFaceFacs)
			{
				BMLFaceFacs face = (BMLFaceFacs)block;

			}
			else if (block is BMLFaceLexeme)
			{
				BMLFaceLexeme face = (BMLFaceLexeme)block;

			}
			else if (block is BMLFaceShift)
			{
				BMLFaceShift face = (BMLFaceShift)block;

			}

			else if (block is BMLGaze)
			{
				BMLGaze gaze = (BMLGaze)block;

			}
			else if (block is BMLGazeShift)
			{
				BMLGazeShift gazeShift = (BMLGazeShift)block;

			}

			else if (block is BMLGesture)
			{
				BMLGesture gesture = (BMLGesture)block;

			}
			else if (block is BMLPointing)
			{
				BMLPointing pointing = (BMLPointing)block;

			}

			else if (block is BMLHead)
			{
				BMLHead head = (BMLHead)block;


			}
			else if (block is BMLHeadDirectionShift)
			{
				BMLHeadDirectionShift headDirectionShift = (BMLHeadDirectionShift)block;

			}

			else if (block is BMLLocomotion)
			{
				BMLLocomotion locomotion = (BMLLocomotion)block;

			}

			else if (block is BMLPosture)
			{
				BMLPosture posture = (BMLPosture)block;

			}
			else if (block is BMLPostureShift)
			{
				BMLPostureShift postureShift = (BMLPostureShift)block;

			}
			else if (block is BMLStance)
			{
				BMLStance stance = (BMLStance)block;

			}
			else if (block is BMLPose)
			{
				BMLPose pose = (BMLPose)block;

			}

			else if (block is BMLSpeech)
			{
				BMLSpeech speech = (BMLSpeech)block;

			}
		}
		
If you want to trigger the synchronization point from Unity, you can call this function

        bml.TriggerSyncPoint(behaviorId, eventName);

