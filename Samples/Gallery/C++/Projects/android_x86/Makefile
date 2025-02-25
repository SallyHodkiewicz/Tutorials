# GNU Make project for 'Samples.Gallery'

# Parallel builds can be enabled using the environment variable MAKEFLAGS (eg: MAKEFLAGS="-j 4")
# For parallel execution in Windows, Make 4.0 or better is required

# Environment variable 'ANDROID_NDK' must point to NDK (eg: C:\Android\SDK\ndk-bundle)
# Environment variable 'ANDROID_PLATFORM' must point to active platform (eg: C:\Android\SDK\platforms\android-30)
# Toolchain (clang++), Java (javac) and Android Build Tools (dx, aapt, zipalign, apksigner) binaries must be added to 'PATH' environment variable

CC = i686-linux-android17-clang
CXX = i686-linux-android17-clang++
AR = i686-linux-android-ar

CFLAGS_COMMON = -g -pipe -Wall -Werror -Wfatal-errors -Wtype-limits -fvisibility=hidden -fmerge-all-constants
CXXFLAGS_COMMON = $(CFLAGS_COMMON) -std=c++11 -fno-exceptions -frtti -fvisibility-inlines-hidden -fno-threadsafe-statics
LDFLAGS_COMMON = -Wextra -static-libstdc++

SHELLTYPE = msdos
ifeq (, $(ComSpec)$(COMSPEC))
  SHELLTYPE = posix
endif
ifeq (/bin, $(findstring /bin, $(SHELL)))
  SHELLTYPE = posix
endif
ifeq (/bin, $(findstring /bin, $(MAKESHELL)))
  SHELLTYPE = posix
endif

ifeq (posix, $(SHELLTYPE))
  DEVNUL = /dev/null
  WHICH = which
  MKDIR = mkdir -p "$(1)"
  BIN2H = ../../../../../Tools/Bin2h/bin2h.py
  CP = cp "$(1)" "$(2)"
  MV = mv "$(1)" "$(2)"
  RM = rm -f "$(1)"
  RMTREE = rm -rf "$(1)"
  FIXSLASHES = 
else
  DEVNUL = NUL
  WHICH = where
  MKDIR = mkdir "$(subst /,\,$(1))" 2> nul || exit 0
  BIN2H = ..\..\..\..\..\Tools\Bin2h\bin2h.exe
  CP = copy /Y "$(subst /,\,$(1))" "$(subst /,\,$(2))" > nul
  MV = move /Y "$(subst /,\,$(1))" "$(subst /,\,$(2))" > nul
  RM = del /Q "$(subst /,\,$(1))" 2> nul || exit 0
  RMTREE = rmdir /S /Q "$(subst /,\,$(1))" 2> nul || exit 0
  SED = ..\..\..\..\..\Tools\sed\sed.exe
  FIXSLASHES = $(SED) -i "s/\(\S\)\\\(\S\)/\1\/\2/g" "$(1)"
endif

ifeq (, $(shell ${WHICH} $(CC) 2> $(DEVNUL) ))
$(error $(CC) not found in PATH)
endif

ifeq (, $(shell ${WHICH} $(CXX) 2> $(DEVNUL) ))
$(error $(CXX) not found in PATH)
endif

ifeq ($(V), 1)
  Q =
else
  Q = @
endif

ifndef CONFIG
  CONFIG = Release
endif

ifeq ($(CONFIG), Debug)
  TARGET_DIR = ../../../../../../Bin/android_x86
  TARGET = ../../../../../../Bin/android_x86/libSamples_Gallery.so
  TARGET_APK = ../../../../../../Bin/android_x86/Samples.Gallery.apk
  INTERMEDIATE = build/Debug
  LIB_DIRS = 
  LIBS = -lNoesisApp -landroid -lNoesis -llog
  LIBS_DEPS = ../../../../../../Bin/android_x86/libNoesis.so ../../../../../../Bin/android_x86/libNoesisApp.so
  INCLUDES = -I../../../../../../Include -I../../../../App/ApplicationLauncher/Include -I../../../../App/DisplayLauncher/Include -I../../../../App/Display/Include -I../../../../App/Interactivity/Include -I../../../../App/Launcher/Include -I../../../../App/MediaElement/Include -I../../../../App/Providers/Include -Ibuild/Debug -I$(ANDROID_NDK)/sources/android/native_app_glue
  DEFINES = -DNS_BUILD -DNS_CONFIG=Debug -DNS_VERSION=3.1.0 -DNS_APP_FRAMEWORK -DNS_LICENSE -DNS_DEBUG -DNS_PROFILE -DNS_MINIMUM_LOG_LEVEL=1
  CFLAGS = $(CFLAGS_COMMON) -D_DEBUG
  CXXFLAGS = $(CXXFLAGS_COMMON) -D_DEBUG
  LDFLAGS = $(LDFLAGS_COMMON) $(CXXFLAGS)
  AAPT_FLAGS = --debug-mode
else ifeq ($(CONFIG), Profile)
  TARGET_DIR = ../../../../../../Bin/android_x86
  TARGET = ../../../../../../Bin/android_x86/libSamples_Gallery.so
  TARGET_APK = ../../../../../../Bin/android_x86/Samples.Gallery.apk
  INTERMEDIATE = build/Profile
  LIB_DIRS = 
  LIBS = -lNoesisApp -landroid -lNoesis -llog
  LIBS_DEPS = ../../../../../../Bin/android_x86/libNoesis.so ../../../../../../Bin/android_x86/libNoesisApp.so
  INCLUDES = -I../../../../../../Include -I../../../../App/ApplicationLauncher/Include -I../../../../App/DisplayLauncher/Include -I../../../../App/Display/Include -I../../../../App/Interactivity/Include -I../../../../App/Launcher/Include -I../../../../App/MediaElement/Include -I../../../../App/Providers/Include -Ibuild/Profile -I$(ANDROID_NDK)/sources/android/native_app_glue
  DEFINES = -DNS_BUILD -DNS_CONFIG=Profile -DNS_VERSION=3.1.0 -DNS_APP_FRAMEWORK -DNS_LICENSE -DNS_PROFILE -DNS_MINIMUM_LOG_LEVEL=2
  CFLAGS = $(CFLAGS_COMMON) -Ofast -DNDEBUG -ffunction-sections -fdata-sections -fno-asynchronous-unwind-tables -U_FORTIFY_SOURCE
  CXXFLAGS = $(CXXFLAGS_COMMON) -Ofast -DNDEBUG -ffunction-sections -fdata-sections -fno-asynchronous-unwind-tables -U_FORTIFY_SOURCE
  LDFLAGS = $(LDFLAGS_COMMON) $(CXXFLAGS) -fuse-ld=gold -Wl,-O3,--gc-sections,--icf=all
  AAPT_FLAGS = --debug-mode
else ifeq ($(CONFIG), Release)
  TARGET_DIR = ../../../../../../Bin/android_x86
  TARGET = ../../../../../../Bin/android_x86/libSamples_Gallery.so
  TARGET_APK = ../../../../../../Bin/android_x86/Samples.Gallery.apk
  INTERMEDIATE = build/Release
  LIB_DIRS = 
  LIBS = -lNoesisApp -landroid -lNoesis -llog
  LIBS_DEPS = ../../../../../../Bin/android_x86/libNoesis.so ../../../../../../Bin/android_x86/libNoesisApp.so
  INCLUDES = -I../../../../../../Include -I../../../../App/ApplicationLauncher/Include -I../../../../App/DisplayLauncher/Include -I../../../../App/Display/Include -I../../../../App/Interactivity/Include -I../../../../App/Launcher/Include -I../../../../App/MediaElement/Include -I../../../../App/Providers/Include -Ibuild/Release -I$(ANDROID_NDK)/sources/android/native_app_glue
  DEFINES = -DNS_BUILD -DNS_CONFIG=Release -DNS_VERSION=3.1.0 -DNS_APP_FRAMEWORK -DNS_LICENSE
  CFLAGS = $(CFLAGS_COMMON) -Ofast -flto -DNDEBUG -ffunction-sections -fdata-sections -fno-asynchronous-unwind-tables -U_FORTIFY_SOURCE -fomit-frame-pointer
  CXXFLAGS = $(CXXFLAGS_COMMON) -Ofast -flto -DNDEBUG -ffunction-sections -fdata-sections -fno-asynchronous-unwind-tables -U_FORTIFY_SOURCE -fomit-frame-pointer
  LDFLAGS = $(LDFLAGS_COMMON) $(CXXFLAGS) -fuse-ld=gold -Wl,-O3,--gc-sections,--icf=all
  AAPT_FLAGS = 
else
  $(error Invalid configuration '$(CONFIG)')
endif

PCH =
PCHFLAGS =
DATA = $(INTERMEDIATE)/App.xaml.bin.h $(INTERMEDIATE)/MainWindow.xaml.bin.h $(INTERMEDIATE)/Resources.xaml.bin.h $(INTERMEDIATE)/Button.xaml.bin.h $(INTERMEDIATE)/RepeatButton.xaml.bin.h $(INTERMEDIATE)/ToggleButton.xaml.bin.h $(INTERMEDIATE)/CheckBox.xaml.bin.h $(INTERMEDIATE)/RadioButton.xaml.bin.h $(INTERMEDIATE)/Slider.xaml.bin.h $(INTERMEDIATE)/TextBlock.xaml.bin.h $(INTERMEDIATE)/TextBox.xaml.bin.h $(INTERMEDIATE)/PasswordBox.xaml.bin.h $(INTERMEDIATE)/Hyperlink.xaml.bin.h $(INTERMEDIATE)/ItemsControl.xaml.bin.h $(INTERMEDIATE)/ComboBox.xaml.bin.h $(INTERMEDIATE)/ListBox.xaml.bin.h $(INTERMEDIATE)/ListView.xaml.bin.h $(INTERMEDIATE)/TreeView.xaml.bin.h $(INTERMEDIATE)/TabControl.xaml.bin.h $(INTERMEDIATE)/Canvas.xaml.bin.h $(INTERMEDIATE)/StackPanel.xaml.bin.h $(INTERMEDIATE)/WrapPanel.xaml.bin.h $(INTERMEDIATE)/DockPanel.xaml.bin.h $(INTERMEDIATE)/Grid.xaml.bin.h $(INTERMEDIATE)/UniformGrid.xaml.bin.h $(INTERMEDIATE)/GroupBox.xaml.bin.h $(INTERMEDIATE)/Expander.xaml.bin.h $(INTERMEDIATE)/ScrollViewer.xaml.bin.h $(INTERMEDIATE)/Menu.xaml.bin.h $(INTERMEDIATE)/ContextMenu.xaml.bin.h $(INTERMEDIATE)/ToolBar.xaml.bin.h $(INTERMEDIATE)/StatusBar.xaml.bin.h $(INTERMEDIATE)/ProgressBar.xaml.bin.h $(INTERMEDIATE)/ToolTip.xaml.bin.h $(INTERMEDIATE)/Brushes.xaml.bin.h $(INTERMEDIATE)/Image.xaml.bin.h $(INTERMEDIATE)/Effects.xaml.bin.h $(INTERMEDIATE)/Blending.xaml.bin.h $(INTERMEDIATE)/Animation.xaml.bin.h $(INTERMEDIATE)/Muli-Regular.ttf.bin.h $(INTERMEDIATE)/Muli-Bold.ttf.bin.h $(INTERMEDIATE)/Muli-Italic.ttf.bin.h $(INTERMEDIATE)/Caladea-Regular.ttf.bin.h $(INTERMEDIATE)/CourierPrime-Regular.ttf.bin.h $(INTERMEDIATE)/Aero\ Matics\ Regular.ttf.bin.h $(INTERMEDIATE)/WidgetIcons.ttf.bin.h $(INTERMEDIATE)/file.png.bin.h $(INTERMEDIATE)/folder-closed.png.bin.h $(INTERMEDIATE)/folder-open.png.bin.h $(INTERMEDIATE)/recycling-bin.png.bin.h $(INTERMEDIATE)/floppy-disk.png.bin.h $(INTERMEDIATE)/search.png.bin.h $(INTERMEDIATE)/Nature.png.bin.h

.SUFFIXES:
.DELETE_ON_ERROR:
.PHONY: all prebuild data clean

all: prebuild $(TARGET_APK)

prebuild:
	@echo ==== [Samples.Gallery] Building '$(CONFIG)' configuration ====
ifndef ANDROID_NDK
	$(error Environment variable ANDROID_NDK not set)
endif
ifndef ANDROID_PLATFORM
	$(error Environment variable ANDROID_PLATFORM not set)
endif

data: $(DATA)

$(INTERMEDIATE):
	$(Q)$(call MKDIR,$(INTERMEDIATE))

$(TARGET_DIR):
	$(Q)$(call MKDIR,$(TARGET_DIR))

$(INTERMEDIATE)/android_native_app_glue.o: $(ANDROID_NDK)/sources/android/native_app_glue/android_native_app_glue.c | $(INTERMEDIATE)
	@echo [CC] $(notdir $<)
	$(Q)$(CC) $(CFLAGS) $(INCLUDES) $(DEFINES) -march=i686 -mtune=intel -mssse3 -mfpmath=sse -m32 -fPIC -c -MMD -MF $(basename $@).d.tmp -MP -o $@ $< && $(call MV,$(basename $@).d.tmp,$(basename $@).d)

	$(Q)$(call FIXSLASHES,$(@:.o=.d))

$(INTERMEDIATE)/%.o: ../../../../Samples/Gallery/Src/%.cpp $(PCH) | $(INTERMEDIATE) data
	@echo [CXX] [Samples/Gallery] $(notdir $<)
	$(Q)$(CXX) $(CXXFLAGS) $(PCHFLAGS) $(INCLUDES) $(DEFINES) -march=i686 -mtune=intel -mssse3 -mfpmath=sse -m32 -fPIC -c -MMD -MF $(basename $@).d.tmp -MP -o $@ $< && $(call MV,$(basename $@).d.tmp,$(basename $@).d)

	$(Q)$(call FIXSLASHES,$(@:.o=.d))

$(INTERMEDIATE)/%.o: ../../../../Samples/Gallery/Src/%.c | $(INTERMEDIATE) data
	@echo [CC] [Samples/Gallery] $(notdir $<)
	$(Q)$(CC) $(CFLAGS) $(INCLUDES) $(DEFINES) -march=i686 -mtune=intel -mssse3 -mfpmath=sse -m32 -fPIC -c -MMD -MF $(basename $@).d.tmp -MP -o $@ $< && $(call MV,$(basename $@).d.tmp,$(basename $@).d)

	$(Q)$(call FIXSLASHES,$(@:.o=.d))

$(INTERMEDIATE)/App.xaml.bin.h: ../../../../Samples/Gallery/Data/App.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/App.xaml" > "$(INTERMEDIATE)/App.xaml.bin.h" 

$(INTERMEDIATE)/MainWindow.xaml.bin.h: ../../../../Samples/Gallery/Data/MainWindow.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/MainWindow.xaml" > "$(INTERMEDIATE)/MainWindow.xaml.bin.h" 

$(INTERMEDIATE)/Resources.xaml.bin.h: ../../../../Samples/Gallery/Data/Resources.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Resources.xaml" > "$(INTERMEDIATE)/Resources.xaml.bin.h" 

$(INTERMEDIATE)/Button.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Button.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Button.xaml" > "$(INTERMEDIATE)/Button.xaml.bin.h" 

$(INTERMEDIATE)/RepeatButton.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/RepeatButton.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/RepeatButton.xaml" > "$(INTERMEDIATE)/RepeatButton.xaml.bin.h" 

$(INTERMEDIATE)/ToggleButton.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ToggleButton.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ToggleButton.xaml" > "$(INTERMEDIATE)/ToggleButton.xaml.bin.h" 

$(INTERMEDIATE)/CheckBox.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/CheckBox.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/CheckBox.xaml" > "$(INTERMEDIATE)/CheckBox.xaml.bin.h" 

$(INTERMEDIATE)/RadioButton.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/RadioButton.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/RadioButton.xaml" > "$(INTERMEDIATE)/RadioButton.xaml.bin.h" 

$(INTERMEDIATE)/Slider.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Slider.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Slider.xaml" > "$(INTERMEDIATE)/Slider.xaml.bin.h" 

$(INTERMEDIATE)/TextBlock.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/TextBlock.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/TextBlock.xaml" > "$(INTERMEDIATE)/TextBlock.xaml.bin.h" 

$(INTERMEDIATE)/TextBox.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/TextBox.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/TextBox.xaml" > "$(INTERMEDIATE)/TextBox.xaml.bin.h" 

$(INTERMEDIATE)/PasswordBox.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/PasswordBox.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/PasswordBox.xaml" > "$(INTERMEDIATE)/PasswordBox.xaml.bin.h" 

$(INTERMEDIATE)/Hyperlink.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Hyperlink.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Hyperlink.xaml" > "$(INTERMEDIATE)/Hyperlink.xaml.bin.h" 

$(INTERMEDIATE)/ItemsControl.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ItemsControl.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ItemsControl.xaml" > "$(INTERMEDIATE)/ItemsControl.xaml.bin.h" 

$(INTERMEDIATE)/ComboBox.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ComboBox.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ComboBox.xaml" > "$(INTERMEDIATE)/ComboBox.xaml.bin.h" 

$(INTERMEDIATE)/ListBox.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ListBox.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ListBox.xaml" > "$(INTERMEDIATE)/ListBox.xaml.bin.h" 

$(INTERMEDIATE)/ListView.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ListView.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ListView.xaml" > "$(INTERMEDIATE)/ListView.xaml.bin.h" 

$(INTERMEDIATE)/TreeView.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/TreeView.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/TreeView.xaml" > "$(INTERMEDIATE)/TreeView.xaml.bin.h" 

$(INTERMEDIATE)/TabControl.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/TabControl.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/TabControl.xaml" > "$(INTERMEDIATE)/TabControl.xaml.bin.h" 

$(INTERMEDIATE)/Canvas.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Canvas.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Canvas.xaml" > "$(INTERMEDIATE)/Canvas.xaml.bin.h" 

$(INTERMEDIATE)/StackPanel.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/StackPanel.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/StackPanel.xaml" > "$(INTERMEDIATE)/StackPanel.xaml.bin.h" 

$(INTERMEDIATE)/WrapPanel.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/WrapPanel.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/WrapPanel.xaml" > "$(INTERMEDIATE)/WrapPanel.xaml.bin.h" 

$(INTERMEDIATE)/DockPanel.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/DockPanel.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/DockPanel.xaml" > "$(INTERMEDIATE)/DockPanel.xaml.bin.h" 

$(INTERMEDIATE)/Grid.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Grid.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Grid.xaml" > "$(INTERMEDIATE)/Grid.xaml.bin.h" 

$(INTERMEDIATE)/UniformGrid.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/UniformGrid.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/UniformGrid.xaml" > "$(INTERMEDIATE)/UniformGrid.xaml.bin.h" 

$(INTERMEDIATE)/GroupBox.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/GroupBox.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/GroupBox.xaml" > "$(INTERMEDIATE)/GroupBox.xaml.bin.h" 

$(INTERMEDIATE)/Expander.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Expander.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Expander.xaml" > "$(INTERMEDIATE)/Expander.xaml.bin.h" 

$(INTERMEDIATE)/ScrollViewer.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ScrollViewer.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ScrollViewer.xaml" > "$(INTERMEDIATE)/ScrollViewer.xaml.bin.h" 

$(INTERMEDIATE)/Menu.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Menu.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Menu.xaml" > "$(INTERMEDIATE)/Menu.xaml.bin.h" 

$(INTERMEDIATE)/ContextMenu.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ContextMenu.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ContextMenu.xaml" > "$(INTERMEDIATE)/ContextMenu.xaml.bin.h" 

$(INTERMEDIATE)/ToolBar.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ToolBar.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ToolBar.xaml" > "$(INTERMEDIATE)/ToolBar.xaml.bin.h" 

$(INTERMEDIATE)/StatusBar.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/StatusBar.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/StatusBar.xaml" > "$(INTERMEDIATE)/StatusBar.xaml.bin.h" 

$(INTERMEDIATE)/ProgressBar.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ProgressBar.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ProgressBar.xaml" > "$(INTERMEDIATE)/ProgressBar.xaml.bin.h" 

$(INTERMEDIATE)/ToolTip.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/ToolTip.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/ToolTip.xaml" > "$(INTERMEDIATE)/ToolTip.xaml.bin.h" 

$(INTERMEDIATE)/Brushes.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Brushes.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Brushes.xaml" > "$(INTERMEDIATE)/Brushes.xaml.bin.h" 

$(INTERMEDIATE)/Image.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Image.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Image.xaml" > "$(INTERMEDIATE)/Image.xaml.bin.h" 

$(INTERMEDIATE)/Effects.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Effects.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Effects.xaml" > "$(INTERMEDIATE)/Effects.xaml.bin.h" 

$(INTERMEDIATE)/Blending.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Blending.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Blending.xaml" > "$(INTERMEDIATE)/Blending.xaml.bin.h" 

$(INTERMEDIATE)/Animation.xaml.bin.h: ../../../../Samples/Gallery/Data/Samples/Animation.xaml | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Animation.xaml" > "$(INTERMEDIATE)/Animation.xaml.bin.h" 

$(INTERMEDIATE)/Muli-Regular.ttf.bin.h: ../../../../Samples/Gallery/Data/Samples/Fonts/Muli-Regular.ttf | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Fonts/Muli-Regular.ttf" > "$(INTERMEDIATE)/Muli-Regular.ttf.bin.h" 

$(INTERMEDIATE)/Muli-Bold.ttf.bin.h: ../../../../Samples/Gallery/Data/Samples/Fonts/Muli-Bold.ttf | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Fonts/Muli-Bold.ttf" > "$(INTERMEDIATE)/Muli-Bold.ttf.bin.h" 

$(INTERMEDIATE)/Muli-Italic.ttf.bin.h: ../../../../Samples/Gallery/Data/Samples/Fonts/Muli-Italic.ttf | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Fonts/Muli-Italic.ttf" > "$(INTERMEDIATE)/Muli-Italic.ttf.bin.h" 

$(INTERMEDIATE)/Caladea-Regular.ttf.bin.h: ../../../../Samples/Gallery/Data/Samples/Fonts/Caladea-Regular.ttf | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Fonts/Caladea-Regular.ttf" > "$(INTERMEDIATE)/Caladea-Regular.ttf.bin.h" 

$(INTERMEDIATE)/CourierPrime-Regular.ttf.bin.h: ../../../../Samples/Gallery/Data/Samples/Fonts/CourierPrime-Regular.ttf | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Fonts/CourierPrime-Regular.ttf" > "$(INTERMEDIATE)/CourierPrime-Regular.ttf.bin.h" 

$(INTERMEDIATE)/Aero\ Matics\ Regular.ttf.bin.h: ../../../../Samples/Gallery/Data/Samples/Fonts/Aero\ Matics\ Regular.ttf | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Fonts/Aero Matics Regular.ttf" > "$(INTERMEDIATE)/Aero Matics Regular.ttf.bin.h" 

$(INTERMEDIATE)/WidgetIcons.ttf.bin.h: ../../../../Samples/Gallery/Data/Samples/Fonts/WidgetIcons.ttf | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Fonts/WidgetIcons.ttf" > "$(INTERMEDIATE)/WidgetIcons.ttf.bin.h" 

$(INTERMEDIATE)/file.png.bin.h: ../../../../Samples/Gallery/Data/Samples/Images/file.png | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Images/file.png" > "$(INTERMEDIATE)/file.png.bin.h" 

$(INTERMEDIATE)/folder-closed.png.bin.h: ../../../../Samples/Gallery/Data/Samples/Images/folder-closed.png | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Images/folder-closed.png" > "$(INTERMEDIATE)/folder-closed.png.bin.h" 

$(INTERMEDIATE)/folder-open.png.bin.h: ../../../../Samples/Gallery/Data/Samples/Images/folder-open.png | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Images/folder-open.png" > "$(INTERMEDIATE)/folder-open.png.bin.h" 

$(INTERMEDIATE)/recycling-bin.png.bin.h: ../../../../Samples/Gallery/Data/Samples/Images/recycling-bin.png | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Images/recycling-bin.png" > "$(INTERMEDIATE)/recycling-bin.png.bin.h" 

$(INTERMEDIATE)/floppy-disk.png.bin.h: ../../../../Samples/Gallery/Data/Samples/Images/floppy-disk.png | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Images/floppy-disk.png" > "$(INTERMEDIATE)/floppy-disk.png.bin.h" 

$(INTERMEDIATE)/search.png.bin.h: ../../../../Samples/Gallery/Data/Samples/Images/search.png | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Images/search.png" > "$(INTERMEDIATE)/search.png.bin.h" 

$(INTERMEDIATE)/Nature.png.bin.h: ../../../../Samples/Gallery/Data/Samples/Images/Nature.png | $(INTERMEDIATE)
	@echo [BIN] [Samples/Gallery] $(notdir $<)
	$(Q)$(BIN2H) "../../../../Samples/Gallery/Data/Samples/Images/Nature.png" > "$(INTERMEDIATE)/Nature.png.bin.h" 

$(TARGET): $(LIBS_DEPS) $(INTERMEDIATE)/android_native_app_glue.o $(INTERMEDIATE)/App.xaml.o $(INTERMEDIATE)/Main.o $(INTERMEDIATE)/MainWindow.xaml.o | $(TARGET_DIR)
	@echo [LD] $(notdir $@)
	+$(Q)$(CXX) $(LDFLAGS) -march=i686 -mtune=intel -mssse3 -mfpmath=sse -m32 -shared -Wl,--no-undefined -Wl,-soname,libSamples_Gallery.so -L../../../../../../Bin/android_x86 $(LIB_DIRS) -o $(TARGET) @$(CONFIG).rsp $(LIBS)
	@echo [STRIP] $(notdir $@)
	$(Q)i686-linux-android-objcopy --only-keep-debug $(TARGET) $(TARGET).debug
	$(Q)i686-linux-android-strip --strip-unneeded $(TARGET)
	$(Q)i686-linux-android-objcopy --add-gnu-debuglink=$(TARGET).debug $(TARGET)

$(INTERMEDIATE)/java/com/noesis/Samples/Gallery/NoesisNativeActivity.class: java/NoesisNativeActivity.java
	@echo [JAVA] $(notdir $<)
	$(Q)$(call MKDIR,$(INTERMEDIATE)/java)
	$(Q)javac -source 1.7 -target 1.7 -Xlint:-options -d $(INTERMEDIATE)/java -classpath "${ANDROID_PLATFORM}/android.jar" -sourcepath $(dir $<) $<

$(INTERMEDIATE)/apk/classes.dex: $(INTERMEDIATE)/java/com/noesis/Samples/Gallery/NoesisNativeActivity.class
	@echo [DEX] $(notdir $@)
	$(Q)$(call MKDIR,$(INTERMEDIATE)/apk)
	$(Q)dx --dex --output=$(INTERMEDIATE)/apk/classes.dex $(INTERMEDIATE)/java

$(INTERMEDIATE)/Samples.Gallery-unsigned.apk: $(TARGET) $(LIBS_DEPS) $(INTERMEDIATE)/apk/classes.dex AndroidManifest.xml
	@echo [AAPT] $(notdir $@)
	$(Q)$(call MKDIR,$(INTERMEDIATE)/apk/lib/x86)
	$(Q)$(call CP,$(TARGET),$(INTERMEDIATE)/apk/lib/x86)
	$(Q)$(call CP,../../../../../../Bin/android_x86/libNoesis.so,$(INTERMEDIATE)/apk/lib/x86)
	$(Q)$(call CP,../../../../../../Bin/android_x86/libNoesisApp.so,$(INTERMEDIATE)/apk/lib/x86)
	$(Q)aapt package -f -S res -M AndroidManifest.xml $(AAPT_FLAGS) -I $(ANDROID_PLATFORM)/android.jar -F $(INTERMEDIATE)/Samples.Gallery-unsigned.apk $(INTERMEDIATE)/apk

$(INTERMEDIATE)/Samples.Gallery-unsigned-aligned.apk: $(INTERMEDIATE)/Samples.Gallery-unsigned.apk
	@echo [ALIGN] $(notdir $@)
	$(Q)zipalign -f 4 $(INTERMEDIATE)/Samples.Gallery-unsigned.apk $(INTERMEDIATE)/Samples.Gallery-unsigned-aligned.apk

$(TARGET_APK): $(INTERMEDIATE)/Samples.Gallery-unsigned-aligned.apk
	@echo [SIGN] $(notdir $@)
	$(Q)apksigner sign --ks android.jks --ks-pass pass:noesis --out $(TARGET_APK) $(INTERMEDIATE)/Samples.Gallery-unsigned-aligned.apk

-include $(INTERMEDIATE)/android_native_app_glue.d $(INTERMEDIATE)/App.xaml.d $(INTERMEDIATE)/Main.d $(INTERMEDIATE)/MainWindow.xaml.d

run:
	$(Q)adb install -r $(TARGET_APK)
	$(Q)adb logcat -c
	$(Q)adb shell monkey -p com.noesis.Samples.Gallery -c android.intent.category.LAUNCHER 1
	$(Q)adb logcat -s Noesis:V

clean:
	@echo ==== [Samples.Gallery] Cleaning '$(CONFIG)' configuration ====
	$(Q)$(call RMTREE,$(INTERMEDIATE))
	$(Q)$(call RM,$(TARGET))
	$(Q)$(call RM,$(TARGET).debug)
	$(Q)$(call RM,$(TARGET_APK))
