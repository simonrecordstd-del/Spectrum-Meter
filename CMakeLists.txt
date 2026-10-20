cmake_minimum_required(VERSION 3.22)
project(SpectrumMeter VERSION 1.0.0)
include(FetchContent)
FetchContent_Declare(JUCE GIT_REPOSITORY https://github.com/juce-framework/JUCE.git GIT_TAG 8.0.6 GIT_SHALLOW TRUE)
FetchContent_MakeAvailable(JUCE)
juce_add_binary_data(SpectrumMeterAssets SOURCES Resources/SpectrumMeter_Background.jpg)
juce_add_plugin(SpectrumMeter COMPANY_NAME "Spectrum Lab" BUNDLE_ID "com.spectrumlab.spectrummeter"
 PLUGIN_MANUFACTURER_CODE SpLb PLUGIN_CODE SpMt FORMATS VST3 PRODUCT_NAME "Spectrum Meter"
 IS_SYNTH FALSE NEEDS_MIDI_INPUT FALSE NEEDS_MIDI_OUTPUT FALSE IS_MIDI_EFFECT FALSE
 EDITOR_WANTS_KEYBOARD_FOCUS FALSE COPY_PLUGIN_AFTER_BUILD FALSE VST3_CATEGORIES Analyzer)
juce_generate_juce_header(SpectrumMeter)
target_sources(SpectrumMeter PRIVATE Source/PluginProcessor.cpp Source/PluginProcessor.h Source/PluginEditor.cpp Source/PluginEditor.h)
target_compile_features(SpectrumMeter PRIVATE cxx_std_17)
target_compile_definitions(SpectrumMeter PUBLIC JUCE_WEB_BROWSER=0 JUCE_USE_CURL=0 JUCE_VST3_CAN_REPLACE_VST2=0)
target_link_libraries(SpectrumMeter PRIVATE SpectrumMeterAssets juce::juce_audio_utils juce::juce_dsp juce::juce_recommended_config_flags juce::juce_recommended_lto_flags juce::juce_recommended_warning_flags)
