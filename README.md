# url_parser.rb
Url Parser Project

class UrlParser 
  def initialize(url)
    @url = url
    @url_split = @url.split('://').last 
    @the_path = @url.split('/').last.split('?').first 
    @the_scheme = @url.split('://').first 
    @the_port = @url.split(':').last.split('/').first
    @the_query = @url.split('?').last.split('#').first.split('&')
  end
  def scheme
    @the_scheme 
  end
  def domain
    @url_split.split(':').first
  end 
  def port
    if @url_split.include?(':')
      @the_port
    elsif @the_scheme == "http"
      "80"
    elsif @the_scheme == "https"
      "443"
    end
  end
  def path 
  @the_path
    if @the_path != ""
      @the_path
    else @the_path == ""  
      nil
    end
  end 
  def query_string
  #For this method I first created an Array "query". 
  #Then I split the URL to get ["q", "cat"], then I split it again to get ["name", "Tim"]
  #I pushed both to "query". Once I had then in the array I called to_h to return a hash with key and values pairs. 
  #{"q"=>"cat", "name"=>"Tim"}
    query = []
    query << @the_query.first.split('=') << @the_query.last.split('=') 
    query.to_h 
  end
  def fragment_id
    @url.split('?').last.split('#').last
  end
end
