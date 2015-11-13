# phpcrawler
phpcrawler forked from phpcrawl.cuab.dewith bug fixed request

# Usage

  <?php
      include("libs/PHPCrawler.class.php");
    
      class MyCrawler extends PHPCrawler 
      {
      function handleDocumentInfo($DocInfo) 
      {
        // Just detect linebreak for output ("\n" in CLI-mode, otherwise "<br>").
        if (PHP_SAPI == "cli") $lb = "\n";
        else $lb = "<br />";
    
        // Print the URL and the HTTP-status-Code
        echo "Page requested: ".$DocInfo->url." (".$DocInfo->http_status_code.")".$lb;
        
        // Print the refering URL
        echo "Referer-page: ".$DocInfo->referer_url.$lb;
        
        // Print if the content of the document was be recieved or not
        if ($DocInfo->received == true)
          echo "Content received: ".$DocInfo->bytes_received." bytes".$lb;
        else
          echo "Content not received".$lb; 
        echo $lb;
        flush();
        } 
      }
  
      $crawler = new MyCrawler();
      $crawler->setURL("www.php.net");
      $crawler->addContentTypeReceiveRule("#text/html#");
      $crawler->addURLFilterRule("#\.(jpg|jpeg|gif|png)$# i");
      $crawler->setTrafficLimit(1000 * 1024);
      $crawler->go();
  ?>
