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

default_platform(:ios)
ENV["FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD"] = "generate a password"

  desc "Create ipa"
  lane :build do
    increment_build_number
    gym
  end

 desc "Upload to App TestFlight"
  lane :upload do
    upload_to_testflight(
    	app_identifier: ENV['BUNDLE_IDENTIFIER'],
    	ipa: "./fastlane/builds/#{ENV['SCHEME']}.ipa",
      skip_waiting_for_build_processing: true
    	)
  end

  desc "Create app ipa and upload to TestFlight"
  lane :do_everything do
    if ENV['SCHEME'] != nil
      build
      upload
    else
      execute_for_all_envs{ do_everything }
    end

  end

  def execute_for_all_envs
    # 1
    schemeList = Dir.glob(".env.*")
    # 2
    schemeList.each do |file|
      # 3
      Dotenv.overload(file)
      # 4
      yield
    end
  end


