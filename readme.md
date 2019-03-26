```
/var/www/hrbiz_dev
/var/www/hrbiz_dev/shared
/var/www/hrbiz_dev/releases
    -- clone project vao thu muc nay 
    VD: git clone https://github.com/abc.git default

/var/www/hrbiz_dev/current --> link den thu muc releases/default
```

https://github.com/komazarari/capistrano-locally

```
set :deploy_to, '/var/www/hrbiz_dev'
set :branch, 'develop'
set :keep_releases, 5

namespace :deploy do	
	before :starting, :vaihang do
		on roles(:app) do

			print "BUILD_NUMBER: #{ENV['BUILD_NUMBER']}\n"
  			ENV['SERVER_TIMESTEMP'] = Time.now.to_i.to_s		
			print "----------- GET TIMESTEMP ON PHP SERVER ------------\n"
			print "SERVER_TIMESTEMP: #{ENV['SERVER_TIMESTEMP']}\n"
			print "----------- GET TIMESTEMP ON PHP SERVER ------------\n"		
		end
  	end

	before :"symlink:release", :run_composer do
		on roles(:app) do
			print "--------- symlink .env file to release directory ------\n"	
			execute "cp /var/www/hrbiz_dev/shared/laradock/.env #{release_path}/laradock/.env"

			# execute "ln -s /var/www/landing_page/topkids.vn/files/ #{release_path}/public/media"

			# print "----------- RUN COMPOSER INSTALL -----------\n"			
			# execute "cd #{release_path}; composer install --no-dev"			
			# print "----------- END COMPOSER INSTALL -----------\n"
			# execute "chmod -R 0777 #{release_path}/storage"
			#print "----------- RUN MIGRATE -----------\n"				
			# execute "cd #{release_path}; php artisan migrate --force"
		end
	end

	after :finishing, :notify do
		on roles(:app) do		
		print "----------- SEND NOTIFICATION TO CHATWORK -----------\n"
		# system("ln -s /var/capistrano/.env #{release_path}/.env")
		end
	end

end

server 'localhost', roles: %w{app web}
```