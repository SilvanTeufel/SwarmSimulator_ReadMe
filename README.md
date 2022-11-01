Copyright 2022 Silvan Teufel / Teufel-Engineering.com All Rights Reserved.

# TopDownRTSTemplate - Readme - 2022

Gameplay Preview:

V 1.0.2
https://www.youtube.com/watch?v=JDpu0PcHnvk

( Mousebot - Added new Character )

V 1.0.1
https://www.youtube.com/watch?v=ZLsuH2VCtrc

(Here you will also find the Random Level Generator added in this Version)

V 1.0.0
https://www.youtube.com/watch?v=hzCgdao3knM


For Questions you can write to info@teufel-engineering.com
If you find any Issues or Bugs i appreciate your Mail!

!!! You can Disable BeginPlay and Tick of my ParentClasses with setting !!!

bool DisableTick = true;
bool DisableBegin = true;

In Blueprint Constructor-Skript. So you are able to only use my Functions and Propertys.

!!! Before Start better fill the Weapontable under Games\UE_5.0\Engine\Plugins\TopDownRTSTemplate\Content\TopDownRTSTemplate\Blueprints\Actors\DT_WeaponData !!!


## Download the Plugin

https://www.unrealengine.com/marketplace/en-US/product/5653ae7bd50e4c52a2ed962ab01e1717

If you have downloaded the plugin it can be found in your Unreal Engine folder:
C:\Program Files\Epic Games\UE_5.0\Engine\Plugins\TopDownRTSTemplate (for example)
If you can find this folder in your enginge plugins folder the download was successful.
If the plugin is in another folder, you should copy it here.

## Install the Plugin

Open Unreal Editor. Click Edit -> Plugins to open the plugin window.
Search for TopDownRTSTemplate and put a check mark at it.

## Import Keyboard Settings

__You can download DefaultInput.ini and GameplayDebuggerTopDownRTSTemplate.ini from here from github by clicking on top left Code->Download Zip__

Open Unreal Editor. Go to Edit -> Project Settings -> AISystem (on left navigation) -> Import.
Choose GameplayDebuggerTopDownRTSTemplate.ini from:
C:\Program Files\Epic Games\UE_5.0\Engine\Plugins\TopDownRTSCamLib\TopDownRTSTemplate\Document\Inputs

__or download from github__

Repeat this step with EngineInputTopDownRTSTemplate.ini .
Open Unreal Editor. Go to Edit -> Project Settings -> Input (on left navigation) -> Import.

If the keybindings are not working you can check the pictures in:
C:\Program Files\Epic Games\UE_5.0\Engine\Plugins\TopDownRTSTemplate\Document\Inputs
and create the keybindings by yourself

## Test Example Map

Open Unreal Editor. Open folder (In Unreal Editor folder tab):
All\Engine\Plugins\TopDownRTSTemplate\Content\TopDownRTSTemplate\Level\levelOne

Open Unreal Editor. Open folder (In Unreal Editor folder tab):
All\Engine\Plugins\TopDownRTSTemplate\Content\TopDownRTSTemplateLevel\levelTwo

## Example Blueprints

Your can find example Blueprints in the Unreal Editor as well:
All\Engine\Plugins\TopDownRTSTemplate\Content\TopDownRTSTemplate\Blueprints

This Blueprints use the Parent Classes from TopDownRTSTemplate Plugin, which you can use for your Blueprints.

## Animation Times

```
You can change the Time the Character stays in Animation-State via Blueprint in Constructor-Skript for example

CharacterBase:
float TeleportStartEndTime = 1.7f;
// When TeleportStartTime reaches TeleportStartEndTime States is changes to StopTeleport

float TeleportStopEndTime = 2.1f; 
// When TeleportStartTime reaches TeleportStopEndTime States is changes to Idle

float ReloadPauseTime = 2.f;
// After Reload is done CharAnimState goes back to Idle

float HitStunnedTime = 0.1f;
// For this Time CharAnimState will stay in isHit

float FirePauseTime;
// This Time is from Weapontable and can be different for every Weapon. CharAnimState is Fire till this Time is reached

EnemyControllerBase:
float EnemyAttackDuration = 0.6f;
float EnemyIsAttackedTime = 0.6f;
float EnemyAttackPauseTime = 1.5f;
```
	
## Parent Classes

If TopDownRTSTemplate is installed the Classes can be used as Parent Class in Blueprint, so all functions from this Class are available.
Just use one of the following Classes as Parent Class and or just choose them in your GameMode Blueprint. Category = TopDownRTSTemplate. 

Parentclasses are:

- CameraBase
- CharacterBase
- EnemyBase
- HUDBase
- ControllerBase
- EnemyControllerBase
- SelectedCharacterIcon
- Spellshield
- UIWeaponIndicator
- Waypoint
- WeaponBase + WeaponTable
- CharacterBaseActionBar
- CharacterBaseHealthBar
- EnemyBaseHealthBar

For CameraBase, if you want only to use the Functions and not run the Code in Tick and BeginPlay (which is automatically setup), just set the Variables to true:

- DisableTick
- DisableBeginPlay

For ControllerBase, if you want to use the Controller, you have to adapt your Settings (Pictures in "Document/Inputs" Folder), or "Import Keyboard Settings" (topic above). You also need GameplayDebuggerTopDownRTSTemplate.ini for the AIController.

---

Here is a List of the Classes and there Functions:

### Class - CharacterBase

```
ACharacterBase(const FObjectInitializer& ObjectInitializer);
virtual void BeginPlay() override;
virtual void Tick(float DeltaTime) override;
virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;
FVector MoveEndLocation; 						// Used for Movement
float Speed = 600.0f;					
float CalcAngle(FVector VectorOne, FVector VectorTwo);  		// Calculations Angel between two Vectors
float CheckAngle(FVector VectorOne, float AngleOneX);    		// Compares Angel between two Vectors
TEnumAsByte<CharacterStatus> CharAnimState;
void setAnimState(TEnumAsByte<CharacterStatus> NewCharAnimState);
TEnumAsByte<CharacterStatus> getAnimState();
FVector ActualLocation;
	
bool DisableTick = false;
bool DisableBeginPlay = false;
	
void onBeginOverlap(class UPrimitiveComponent* HitComp,
class AActor* OtherActor, class UPrimitiveComponent* OtherComp,
int32 OtherBodyIndex, bool bFromSweep, const FHitResult& SweepResult);
FVector ClimbingStartLocation;
class UWidgetComponent* HealthWidgetComp;
float GetHealth();
float GetMaxHealth();
void SetHealth(float NewHealth);
bool Die();
float DeathTime;      							// Time is used for despawn
void SpawnHealthWidget();						// Spawns the Health Widget
float Health;								// Current Health of the Character
float MaxHealth = 120;							// Max Health of the Character
float GetDistance();							
float GetMaxDistance();							
void SetDistance(float NewDistance);
float MaxDistance = 100;
float AvailableDistance;
void SetSelected();							// Sets the Character selected Icon
void SetDeselected();							// Hides the Icon
TArray <FVector> MoveArray;						// Array for moving with shift-click	
int32 MoveArrayIterator;						// Iterator for moving with shift-click	
FVector ForwardVector;
FVector LastDirection;
float JumpHeight = 600.0f;
int DoubleJumpCounter = 0;
void ToggleSpellShield();
void SpawnSpellShield();
void RefreshSpellShieldCounterTick(float deltaTime);
void SpawnSelectedCharacterIcon();
bool Attack(AActor* AttackedCharacter);
float FireTime;
float FirePauseTime;
float ReloadTime;
float ReloadPauseTime = 2.f;
float IsHitTime;
AEnemyBase* TargetedAi;
TSubclassOf<class AWeaponBase> WeaponClass;
class AWeaponBase* Weapon;
void WeaponSpawn();
void ChangeWeapon(FString WeaponName);
void CreateIconActionRadius();
void CreateIconNormalRadius();
class USkeletalMesh* GetWeaponMesh();
TArray<FString> Weapons;
TArray<int> MaxMagSize;
TArray<int> MagSize;
void ReloadWeapon();
int ActualWeaponId = 1;
class ASelectedCharacterIcon* SelectedCharacterIcon;
class ASpellshield* Spellshield;
class UDecalComponent* CursorToWorld;
float TeleportStartTime = 0; // Used Timer
float TeleportStartEndTime = 1.7f; // When TeleportStartTime reaches TeleportStartEndTime States is changes to StopTeleport
float TeleportStopEndTime = 2.1f; // When TeleportStartTime reaches TeleportStopEndTime States is changes to Idle
float TeleportCooldownTime = 0;
float TeleportCooldownStartTime = 30;
float TeleportRadius = 50.f;
float TeleportOutOfRadiusDmg = 10.f;
void CreateTeleportRadius();
void TeleportCoolDownTick(float DeltaSeconds);
```

### Class - EnemyBase

```
AEnemyBase(const FObjectInitializer& ObjectInitializer);
virtual void BeginPlay() override;
virtual void Tick(float DeltaTime) override;
virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;
	
bool DisableTick = false;
bool DisableBeginPlay = false;
	
void isAttacked(AActor* AttackingCharacter); 
void setWalkSpeed(float Speed);
float EnemyNormalWalkspeed = 400.f; 
float EnemySlowWalkspeed = 200.f; 

float AttackTime = 0.0f;
float AttackPauseTime = 0.0f;
float GetAttackedTime = 0.0f;
class AWaypoint* NextWaypoint;
void setWaypoint(class AWaypoint* NewNextWaypoint);
void setAnimState(TEnumAsByte<AiStatus> NewCharAnimState);
TEnumAsByte<AiStatus> getAnimState();
TEnumAsByte<AiStatus> CharAnimState;
AActor* ActorToChase;
void SpawnSelectedCharacterIcon();
void SetSelected();
void SetDeselected();
class ASelectedCharacterIcon* SelectedCharacterIcon;
float GetHealth();
void SetHealth(float NewHealth);
float GetMaxHealth();
class UWidgetComponent* HealthWidgetComp;
float Health;
float MaxHealth = 120;
float DeathTimer = 0;
```


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
