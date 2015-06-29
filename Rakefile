name = "main"
src = "#{name}.tex"
dvi = "#{name}.dvi"
pdf = "#{name}.pdf"

file dvi do
	unless File.exists? src
		puts "#{src} not found!"
		abort
	end
	sh "platex", src
end

file pdf => dvi do
	sh "dvipdf", dvi
end

desc "View the results of compilation with evince."
task :view do
	unless File.exists? pdf
		Rake::Task[pdf].invoke
	end
	sh "xdg-open #{pdf} 2> /dev/null &"
end

require "rake/clean"
CLEAN.include(%w(aux log).map{|x| "*.#{x}"})
CLOBBER.include(%w(pdf dvi).map{|x| "*.#{x}"})

task all: [:clobber, pdf]
task default: :all
