# iphone
icloud lib/commands/current.sh
 @@ -7,20 +7,25 @@ plugin_current_command() {
   search_path=$(pwd)
   local version_and_path
   version_and_path=$(find_version "$plugin_name" "$search_path")
   local version
   version=$(cut -d '|' -f 1 <<< "$version_and_path");
   local full_version
   full_version=$(cut -d '|' -f 1 <<< "$version_and_path");
   local version_file_path
   version_file_path=$(cut -d '|' -f 2  <<< "$version_and_path");

   check_if_version_exists "$plugin_name" "$version"
   check_for_deprecated_plugin "$plugin_name"

   if [ -z "$version" ]; then
   # shellcheck disable=SC2162
   IFS=' ' read -a versions <<< "$full_version"

   if [ ${#versions} -eq 0 ]; then
     printf "%s\\n" "$(display_no_version_set "$plugin_name")"
     exit 126
   else
     printf "%-8s%s\\n" "$version" "(set by $version_file_path)"
   fi

   for version in "${versions[@]}"; do
     check_if_version_exists "$plugin_name" "$version"
     check_for_deprecated_plugin "$plugin_name"
   done
   printf "%-7s%s\\n" "$full_version" " (set by $version_file_path)"
 }

 current_command() { lib/commands/current.sh
 @@ -7,20 +7,25 @@ plugin_current_command() {
   search_path=$(pwd)
   local version_and_path
   version_and_path=$(find_version "$plugin_name" "$search_path")
   local version
   version=$(cut -d '|' -f 1 <<< "$version_and_path");
   local full_version
   full_version=$(cut -d '|' -f 1 <<< "$version_and_path");
   local version_file_path
   version_file_path=$(cut -d '|' -f 2  <<< "$version_and_path");

   check_if_version_exists "$plugin_name" "$version"
   check_for_deprecated_plugin "$plugin_name"

   if [ -z "$version" ]; then
   # shellcheck disable=SC2162
   IFS=' ' read -a versions <<< "$full_version"

   if [ ${#versions} -eq 0 ]; then
     printf "%s\\n" "$(display_no_version_set "$plugin_name")"
     exit 126
   else
     printf "%-8s%s\\n" "$version" "(set by $version_file_path)"
   fi

   for version in "${versions[@]}"; do
     check_if_version_exists "$plugin_name" "$version"
     check_for_deprecated_plugin "$plugin_name"
   done
   printf "%-7s%s\\n" "$full_version" " (set by $version_file_path)"
 }

 current_command() {


