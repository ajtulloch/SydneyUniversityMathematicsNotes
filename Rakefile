task :build do
  require 'fileutils'
  output = "PDFs"
  scratch = "PDFScratch"
  FileUtils.rm_r output
  FileUtils.rm_r scratch
  FileUtils.mkdir_p scratch
  FileUtils.mkdir_p output
  
  begin
    # Create scratch dir
    Dir["**/*.tex"].each do |file|
      FileUtils.cp file, scratch
    end
    
    # Generate PDFs
    Dir.chdir(scratch) do
      FileList["*.tex"].each do |file|
        # We run twice to ensure hyperlinks work correctly
        # FIXME: Is there a better way to do this?
        sh "xelatex '#{file}'"
        sh "xelatex '#{file}'"
        
      end
    end
    
    # Move to clean PDFs directory
    Dir[scratch + "/*.pdf"].each do |pdf_file|
      FileUtils.cp pdf_file, "PDFs"
    end

    # Remove scratch directory
    FileUtils.rm_r "PDFScratch"
  end
end

task :clean do
  require 'fileutils'
  FileUtils.rmdir "PDFScratch"
  FileUtils.rmdir "PDFs"
end
