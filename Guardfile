guard 'livereload' do
  watch("intro_to_cdns.html")
end

regenerate_html = "pandoc -t revealjs intro_to_cdns.markdown -o intro_to_cdns.html -V theme=moon --standalone --slide-level=1"

guard :shell do
  watch('intro_to_cdns.markdown') { `#{regenerate_html}` }
end
