Yanwen Tracking API - Node.js
================================
Use Node.js to track Yanwen shipments with Yanwen Tracking API.

Features
--------
- Real-time Yanwen tracking.
- Batch Yanwen tracking.
- Other features to manage your Yanwen tracking.

Installation
------------

Installation is easy:

    gem install trackingmore

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your Yanwen shipments.

Usage
----------

Create a tracking (Real-time tracking):

      require  'trackingmore'

      TrackingMore.api_key = 'your api key'
      
      begin
        params  = {"tracking_number" => "VR666608345YP","courier_code"=>"yanwen"}
        response = TrackingMore::Tracking.create_tracking(params)
        puts response
      rescue TrackingMore::TrackingMoreException => e
        puts "Caught Custom Exception: #{e.message}"
      rescue StandardError => e
        puts "Caught Standard Error: #{e.message}"
      end


Create trackings (Max. 40 tracking numbers create in one call):

    require  'trackingmore'

    TrackingMore.api_key = 'your api key'
    
    begin
      params  = [{"tracking_number" => "UJ826304125YP","courier_code"=>"yanwen"},{"tracking_number" => "UJ851722358YP","courier_code"=>"yanwen"}]
      response = TrackingMore::Tracking.batch_create_trackings(params)
      puts response
    rescue TrackingMore::TrackingMoreException => e
      puts "Caught Custom Exception: #{e.message}"
    rescue StandardError => e
      puts "Caught Standard Error: #{e.message}"
    end



Get status of the shipment:

    require  'trackingmore'

    TrackingMore.api_key = 'your api key'
    
    begin
      # Perform queries based on various conditions
      # params  = {"tracking_numbers" => "UJ826304125YP","courier_code"=>"yanwen"}
      # params  = {"tracking_numbers" => "UJ826304125YP,UJ851722358YP","courier_code"=>"yanwen"}
      params  = {"created_date_min" => "2023-08-23T14:00:00+08:00","created_date_max"=>"2023-08-23T15:04:00+08:00"}
      response = TrackingMore::Tracking.get_tracking_results(params)
      puts response
    rescue TrackingMore::TrackingMoreException => e
      puts "Caught Custom Exception: #{e.message}"
    rescue StandardError => e
      puts "Caught Standard Error: #{e.message}"
    end


Update a tracking by ID:

    require  'trackingmore'

    TrackingMore.api_key = 'your api key'
    
    begin
      params  = {"customer_name" => "New name","note"=>"New tests order note"}
      id_string = '9bc1bd17696cfbad3c994a032f51ba78'
      response = TrackingMore::Tracking.update_tracking_by_id(id_string, params)
      puts response
    rescue TrackingMore::TrackingMoreException => e
      puts "Caught Custom Exception: #{e.message}"
    rescue StandardError => e
      puts "Caught Standard Error: #{e.message}"
    end