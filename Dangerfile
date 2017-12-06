has_milestone = github.pr_json["milestone"] != nil
warn "あれれ？マイルストーンが設定されてないよ？" unless has_milestone

warn "WIPなの？はやく終わるといいねー！" if github.pr_title.include? "[WIP]" or github.pr_labels.include?("WIP")

####
# Android Lint
####
android_lint.gradle_task = "app:lintDebug"
android_lint.report_file = "app/build/reports/lint-results-debug.xml"
android_lint.filtering = true
android_lint.lint(inline_mode: true)

dir = "app/src/main/java/com/os/operando/android/danger/"

features = { :package1 => "パッケージ1", :package2 => "パッケージ2" }

active_files = (git.modified_files + git.added_files)
f = active_files.select { |file| file.start_with? dir }

f.each do |file|
  features.each do |k,v|
    warn "#{v}" if file.start_with? dir + k
  end
end