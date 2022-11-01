Copyright 2022 Silvan Teufel / Teufel-Engineering.com All Rights Reserved.

# TopDownRTSTemplate - Readme - 2022

Gameplay Preview:


For Questions you can write to info@teufel-engineering.com
If you find any Issues or Bugs i appreciate your Mail!

!!! You can Disable BeginPlay and Tick of my ParentClasses with setting !!!

bool DisableTick = true;
bool DisableBegin = true;

In Blueprint Constructor-Skript. So you are able to use all my Functions and Propertys.

## Download the Plugin

!!! LINK HERE SOON !!!

If you have downloaded the plugin it can be found in your Unreal Engine folder:
C:\Program Files\Epic Games\UE_5.0\Engine\Plugins\SwarmSimulator (for example).
or
C:\Program Files\Epic Games\UE_5.0\Engine\Plugins\Marketplace\SwarmSimulator

If you can find this folder in your enginge plugins folder the download was successful.
If the plugin is in another folder, you should copy it here.

## Install the Plugin

Open Unreal Editor. Click Edit -> Plugins to open the plugin window.
Search for SwarmSimulator and put a check mark at it.

## Import Keyboard Settings

__You can download DefaultInput.ini and SwarmSettings.ini from here from github by clicking on top left Code->Download Zip__

Open Unreal Editor. Go to Edit -> Project Settings -> AISystem (on left navigation) -> Import.
Choose SwarmSettings.ini from:
C:\Program Files\Epic Games\UE_5.0\Engine\Plugins\SwarmSimulator\Document\Inputs

__or download from github__

Repeat this step with DefaultInput.ini .
Open Unreal Editor. Go to Edit -> Project Settings -> Input (on left navigation) -> Import.

If the keybindings are not working you can check the pictures in:
C:\Program Files\Epic Games\UE_5.0\Engine\Plugins\SwarmSimulator\Document\Inputs
and create the keybindings by yourself

## Test Example Map

Open Unreal Editor. Open folder (In Unreal Editor folder tab):
All\Engine\Plugins\SwarmSimulator\Content\SwarmSimulator\Level\levelOne

## Example Blueprints

Your can find example Blueprints in the Unreal Editor as well:
All\Engine\Plugins\SwarmSimulator\Content\SwarmSimulator\Blueprints

This Blueprints use the Parent Classes from SwarmSimulator Plugin, which you can use for your Blueprints.
	
## Parent Classes

If TopDownRTSTemplate is installed the Classes can be used as Parent Class in Blueprint, so all functions from this Class are available.
Just use one of the following Classes as Parent Class and or just choose them in your GameMode Blueprint. Category = TopDownRTSTemplate. 

Parentclasses are:

- CameraBase
- MouseBotBase
- EnemyBase
- HUDBase
- ControllerBase
- EnemyControllerBase
- Waypoint
- MouseBotBaseActionBar
- EnemyBaseHealthBar


For ControllerBase, if you want to use the Controller, you have to adapt your Settings (Pictures in "Document/Inputs" Folder), or "Import Keyboard Settings" (topic above).

---

Here is a List of the Classes and there Functions:

### Class - EnemyBase

```
public:
AEnemyBase(const FObjectInitializer& ObjectInitializer);
class UCapsuleComponent* TriggerCapsule;
void OnOverlapBegin(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, 	const FHitResult& SweepResult);
void OnOverlapEnd(class UPrimitiveComponent* OverlappedComp, class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);
virtual void BeginPlay() override;
virtual void Tick(float DeltaTime) override;
virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;
bool DisableTick = false;
bool DisableBeginPlay = false;
void isAttacked(AActor* AttackingCharacter); // AActor* SelectedCharacter
void setWalkSpeed(float Speed);
float NormalWalkspeed = 400.f; 
float SlowWalkspeed = 200.f; 	
float AttackTime = 0.0f;
float AttackPauseTime = 0.0f;
float GetAttackedTime = 0.0f;
class AWaypoint* NextWaypoint;
void SetWaypoint(class AWaypoint* NewNextWaypoint);
void SetAnimState(TEnumAsByte<AiStatus> NewCharAnimState);
TEnumAsByte<AiStatus> GetAnimState();
TEnumAsByte<AiStatus> CharAnimState;
AActor* ActorToChase;
float GetHealth();
void SetHealth(float NewHealth);
float GetMaxHealth();
class UWidgetComponent* HealthWidgetComp;
float Health;
float MaxHealth = 120;
float DeathTimer = 0;
bool DestroyAfterDeath = false;
```

// Hier weiter
### Class - CameraBase

```
void CreateCameraComp();

USceneComponent* RootScene;

USpringArmComponent* SpringArm;

FRotator SpringArmRotator = FRotator(-50, 0, 0);

 UCameraComponent* CameraComp;

 APlayerController* PC;

 void GetViewPortScreenSizes(int x);
 void SpawnControllWidget();
 
FVector GetCameraPanDirection();

void PanMoveCamera(const FVector& PanDirection);
- Scrolling with Screen Edges This is Called in Tick generaly with CamSpeed: PanMoveCamera(GetCameraPanDirection() \* CamSpeed);

float Margin = 15;

int32 ScreenSizeX;
- Screen Edge For Scrolling with Mouse

int32 ScreenSizeY;
- Screen Edge For Scrolling with Mouse

int GetViewPortScreenSizesState = 1;
- Set 2 for System Resolution, Set 1 for Viewport Edges
- The Function Defines ScreenSize X and Y

float CamSpeed = 80;
- Camspeed for Scrolling with Screen Edges

void ZoomIn();
void ZoomOut();
void ZoomStop();
void CamLeft();
void CamRight();
void CamStop();


void CamRotationTick();
- Is Used For Rotation is generaly called in Tick

void JumpCamera(FHitResult Hit);
- Jump Camera to Hit Position

FVector2D GetMousePos2D();
- Functionality is defined by Functionname

void Zoom();
- Functionality is defined by Functionname

void ZoomOutToPosition();
- Functionality is defined by Functionname

void CamMoveAndZoomTick();
- For Cam Movement and Cam Zoom generaly called in Tick

void ZoomInToPosition();
- Sets ZoomCamOutToPosition to true

void LockOnCharacter(ACharacter\* SelectedActor);
- Lock the Camera to an Actor, ZoomCamOutToPosition is checked

float ZoomOutPosition = 20000.f;
- Cameraposition when ZoomOutToPosition() is called.

float ZoomPosition = 1500.f;
- Cameraposition when ZoomInToPosition() is called.

float PitchValue = 0.f;
- Of the Camera

float YawValue = 0.f;
- Of the Camera

float RollValue = 0.f;
- Of the Camera

bool RollCamRight = false;
- Functionality is defined by Functionname

bool RollCamLeft = false;
- Functionality is defined by Functionname

bool ZoomCamOut = false;
- Functionality is defined by Functionname

bool ZoomCamIn = false;
- Functionality is defined by Functionname

bool ZoomCamOutToPosition = false;
- Functionality is defined by Functionname

bool MoveCamForward = false;
- Functionality is defined by Functionname

bool MoveCamBackward = false;
- Functionality is defined by Functionname

bool MoveCamLeft = false;
- Functionality is defined by Functionname

bool MoveCamRight = false;
- Functionality is defined by Functionname

float startTime = 0.f;
- Functionality is defined by Functionname

int CamAngle = 0;
- Should not be changed. Is to keep Track of actual Angle

bool DisableTick = false;
- Disable My Tick Functions of Parent Class, to use my Function in Blueprint

bool DisableBeginPlay = false;
- Disable BeginPlay Functions of Parent Class, to use my Function in Blueprint

class UWidgetComponent\* ControlWidgetComp;
- Keyboard Widget (which is shown by pressing Tab)

FRotator ControlWidgetRotation = FRotator(50, 180, 0);
- Rotation of The Widget

FVector ControlWidgetLocation = FVector(400.f, -350.0f, -250.0f);
- Location of the Widget when shown

FVector ControlWidgetHideLocation = FVector(400.f, -2500.0f, -250.0f);
- Location of the Widget when hidden

void HideControlWidget();
void ShowControlWidget();


```

---

### Class - HUDBase

```
virtual void DrawHUD();
- Used in Tick() to Draw the Selectionfield and trigger select.

FVector2D InitialPoint;
- Position of mouse on screen when pressed;

FVector2D CurrentPoint;
- Position of mouse on screen while holding;

float RectangleScaleSelectionFactor = 0.9;
- Factor of inner/outer selection field

FVector2D GetMousePos2D();
- Functionality is defined by Functionname

void AimToMouse();
- Actors can be triggert to Look to the Mouse

void MoveActorsThroughWayPoints(TArray <ATopDownExampleCharacter\*> Actors);
- Move Actors through Waypoints

void StartMovingActors(TArray<ATopDownExampleCharacter\*> Actors);
- Start Move Actors.

void setZeroActor(ACharacterBase* Actor);
- Functionality is defined by Functionname

bool bStartSelecting = false;
TArray <ACharacterBase\*> FoundActors;

bool bStartSelectingEnemys = false;

TArray <ACharacterBase*> FoundCharacters;

TArray <AEnemyBase*> FoundEnemys;

bool DisableTick = false;
```
---

### Class - ControllerBase

```
	
bool DisableTick = false;
bool DisableBeginPlay = false;
	
	
void ShiftPressed();
void ShiftReleased();
void LeftClickPressed();
void LeftClickReleased();
void RightClickPressed();
void SpacePressed();
void SpaceReleased();
void QPressed();
void WPressed();
void APressed();
void AReleased();
void EPressed();
void SPressed();
void FPressed();
void RPressed();
void JumpCamera();
void StrgPressed();
void StrgReleased();
void ZoomIn();
void ZoomOut();
void ZoomStop();
void CamLeft();
void CamRight();
void ControllDirectionToMouse(ACharacterBase* SelectedActor);
void ToggleLockCameraToCharacter();
void TabPressed();
void TabReleased();
void CameraPawnForward();
void CameraPawnBackward();
void CameraPawnLeft();
void CameraPawnRight();
void CameraPawnForwardR();
void CameraPawnBackwardR();
void CameraPawnLeftR();
void CameraPawnRightR();
bool IsShiftPressed = false;
bool AIsPressed = false;
bool IsStrgPressed = false;
bool IsSpacePressed = false;
bool LockCameraToCharacter = false;
TArray <ACharacterBase*> SelectedActors;
TArray <ACharacterBase*> MovingActors;
```

### Class - EnemyControllerBase

```
AEnemyControllerBase();
virtual void BeginPlay() override;
virtual void OnPossess(APawn* Pawn) override;
virtual void Tick(float DeltaSeconds) override;
virtual FRotator GetControlRotation() const override;

bool DisableTick = false;
bool DisableBeginPlay = false;
	
void isAttacked(AActor* Actor, FKey ButtonPressed);
void OnPawnDetected(const TArray<AActor*>& DetectedPawns);

float EnemySightRadius = 1500.0f;
float EnemySightAge = 5.0f;
float EnemyLoseSightRadius = EnemySightRadius + 1000.0f;
float EnemyFieldOfView = 90.0f; 
float EnemyDespawnTime = 10.0f;
float EnemyAttackPauseTime = 1.5f;
float EnemyAttackDuration = 0.6f;
float EnemyIsAttackedTime = 0.6f;
float EnemyRecivesDmg = 20.f; 

class UAISenseConfig_Sight* SightConfig;
float bIsPlayerDetected = false;
float DistanceToPlayer = 0.0f;
float DistanceToWaypoint = 0.0f;
float SprintTime = 0.0f;
ACharacterBase* ActorToChase;
```

### Class - EnemyControllerBase

```

AUIWeaponIndicator();
USkeletalMeshComponent* WeaponMesh;
virtual void BeginPlay() override;
virtual void Tick(float DeltaTime) override;
void ChangeWeaponIndicator(class USkeletalMesh* NewWeaponMesh);
FVector WeaponIndicatorPosition = FVector(-500.f, 400.0f, -290.0f); 		// Choose Position of the Weapon Indicator
FRotator WeaponIndicatorRotation = FRotator(-45.f, 0.0f, 0.f); 			// Choose Rotation of the Weapon Indicator
```
