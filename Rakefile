task :default => "build"

desc 'build documentation'
task build: :clean do

  puts "Converting to HTML..."
  `bundle exec asciidoctor './Query Builder.adoc' -o './Query Builder.html'`
  # puts " -- HTML output at SSMS-tips-tricks.html"

  puts "Converting to PDF..."
  `bundle exec asciidoctor-pdf './Query Builder.adoc' -o './Query Builder.pdf' 2>/dev/null`
  # puts " -- PDF  output at SSMS-tips-tricks.pdf"

end # :build

desc 'removes detritus from build folder'
task :clean do
  puts "cleaning..."

  Dir.glob("./build/*") {|file|
    puts "removing #{file}"
    File.delete(file)
  }

end # :clean

# http://stackoverflow.com/questions/15501149/how-can-i-include-a-version-file-in-a-commit
# Read config/version.rb file containing
#   a.b.c
# Overwrite config/version.rb file to contain:
#   a.b.c+1
desc 'increments PATCH by 1 (http://semver.org)'
task :bump do

  file = "./VERSION"
  unless (File.exist?(file))
    $stderr.puts("cannot locate version file #{file}")
  else
    s = File.open(file) {|f| f.read}
    if (s =~ /(\d+)\D+(\d+)\D+(\d+)/)
      # s1 = "VERSION = [#{$1}, #{$2}, #{$3.to_i + 1}]"
      s1 = "#{$1}.#{$2}.#{$3.to_i + 1}"
      $stderr.puts(s1)
      File.open(file, "w") {|f| f.puts(s1) }
    else
      $stderr.puts("cannot parse version file")
    end
  end

end # :bump
