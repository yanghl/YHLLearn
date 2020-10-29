platform :ios, '10.0'
use_frameworks!
source 'https://github.com/CocoaPods/Specs.git'  #官方库
source 'https://github.com/yanghl/seanRepo.git' 

def gitPullModule(moduleName, gitUrl, branchName)
  path = "../#{moduleName}"
  if File.directory?(path)
    Dir.chdir(path) do
      system('git pull')
    end
    pod moduleName, :path => path
    else
    pod moduleName, :git => gitUrl, :branch => branchName
  end
end

def debugDependence
  # pod 'GWCommonComponent', :git => 'https://gitlab.btpoc.com/app/ios/gwcommoncomponent.git', :branch => "develop"
end

def releaseDependence
  # pod 'GWAPIManager', '0.4.288'
end

target 'YHLLearn' do
  # 自己电脑跑代码就把这个打开
  debugDependence
  # 自己电脑跑代码就把这个注释掉
  #    releaseDependence
  pod 'YHLCore'
end

post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['ENABLE_BITCODE'] = 'NO'
      config.build_settings['VALID_ARCHS'] = 'arm64 arm64e armv7s'
      if config.name == 'Debug'
        config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] = '$(inherited) DEBUG=1 DEBUG_ADHOC=1 COCOAPODS=1'
        config.build_settings['SWIFT_ACTIVE_COMPILATION_CONDITIONS'] = '－D $(inherited) DEBUG DEBUG_ADHOC COCOAPODS'
        config.build_settings['ONLY_ACTIVE_ARCH'] = 'YES'
        config.build_settings['DEBUG_INFORMATION_FORMAT'] = 'dwarf'
        config.build_settings['SWIFT_OPTIMIZATION_LEVEL'] = '-Onone'
        config.build_settings['GCC_OPTIMIZATION_LEVEL'] = '0'
        config.build_settings['SWIFT_COMPILATION_MODE'] = 'singlefile'
        config.build_settings['MTL_ENABLE_DEBUG_INFO'] = 'INCLUDE_SOURCE'
      end
      if config.name == 'Release'
        config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] = '$(inherited) RELEASE_APPSTORE=1 COCOAPODS=1'
        config.build_settings['SWIFT_ACTIVE_COMPILATION_CONDITIONS'] = '－D $(inherited) RELEASE_APPSTORE COCOAPODS'
      end
    end
  end
end
