# This file contains the fastlane.tools configuration
# You can find the documentation at https://docs.fastlane.tools
#
# For a list of all available actions, check out
#
#     https://docs.fastlane.tools/actions
#
# For a list of all available plugins, check out
#
#     https://docs.fastlane.tools/plugins/available-plugins
#

# Uncomment the line if you want fastlane to automatically update itself
# update_fastlane

default_platform(:android)

platform :android do
  desc "Output configuration for debugging"
  lane :config do
    puts is_ci
    sh("fastlane --version")
    gradle(task: "--version")
    sh("fastlane lanes")
    gradle(task: "tasks")
    gradle(task: "model")
    gradle(task: "projects")
    gradle(task: "properties")
  end

  desc "Compile debug sources"
  lane :compile do
    gradle(task: "compileDebugSources")
    gradle(task: "compileDebugUnitTestSources")
    gradle(task: "compileDebugAndroidTestSources")
  end

  desc "Android lint"
  lane :lint do
    gradle(task: "lintDebug")
  end

  desc "Assemble source and test APK"
  lane :assemble do
    gradle(task: "assembleDebug")
    gradle(task: "assembleDebugAndroidTest")
  end

  desc "Unit test"
  lane :unit_test do
    gradle(task: "testDebugUnitTest")
  end

  desc "Instrumentation test"
  lane :instrumentation_test do
    automated_test_emulator_run(
      AVD_setup_path: "fastlane/AVD_setup.json",
      AVD_recreate_new: false,
      AVD_clean_after: false,
      gradle_task: "connectedDebugAndroidTest")
  end

  desc "Local pipeline execution"
  lane :pipeline do
    compile
    lint
    assemble
    unit_test
    instrumentation_test
    notification(subtitle: "Pipeline finished", message: "Execution successful.")
  end
end