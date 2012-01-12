require 'rake'
require 'twilio-ruby'
require 'yaml'

task :default => [:send_sms]

desc "Send a given SMS message to a given phone number."
task :send_sms do |t|
  unless ENV['phone_number']
    $stderr.puts 'Set a destination phone number using a "phone_number" ENV variable.'
    $stderr.puts '  e.g. phone_number=1111111111 rake send_sms'
    exit
  end
  unless ENV['message']
    $stderr.puts 'Set a text message using a "message" ENV variable.'
    $stderr.puts '  e.g. message="test text" rake send_sms'
    exit
  end

  phone_number = ENV['phone_number'].gsub(/[^\d]/, '')
  message = ENV['message']

  twilio_config = YAML.load(File.read('config/twilio.yml'))
  @client = Twilio::REST::Client.new twilio_config['account_sid'], twilio_config['auth_token']
  @client.account.sms.messages.create(
    :from => twilio_config['from_phone_number'],
    :to => "+1#{phone_number}",
    :body => message
  )
end
