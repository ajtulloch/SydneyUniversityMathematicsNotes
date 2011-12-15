task :build do
  require 'fileutils'
  FileUtils.rmdir "PDFScratch"
  FileUtils.rmdir "PDFs"
  FileUtils.mkdir_p "PDFScratch"
  FileUtils.mkdir_p "PDFs"
  
  begin
    # Create scratch dir
    tex_files = Dir["**/*.tex"]
    tex_files.each do |file|
      FileUtils.cp file, "PDFScratch"      
    end
    
    # Generate PDFs
    Dir.chdir("PDFScratch") do
      tex_files = FileList["*.tex"]
      tex_files.each do |file|
        sh "xelatex '#{file}'"
      end
    end
    
    
    pdf_files = Dir["PDFScratch/*.pdf"]
    pdf_files.each do |pdf_file|
      FileUtils.cp pdf_file, "PDFs"
    end
    
    FileUtils.rm_r "PDFScratch"
    # Remove waste created by LaTeX 
    # pdf_files = Dir["PDFScratch/*.tex"]
    # pdf_files.each do |file|
    #   FileUtils.mv file, "PDFScratch"      
    #   
  end
end

task :clean do
  require 'fileutils'
  FileUtils.rmdir "PDFScratch"
  FileUtils.rmdir "PDFs"
end
