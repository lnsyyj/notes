	radosgw-admin metadata get user:yujiang
	{
	    "key": "user:yujiang",
	    "ver": {
	        "tag": "_3JOReJbi_1UWkHi2GtYC5Fl",
	        "ver": 1
	    },
	    "mtime": "2016-08-15 01:53:26.633037Z",
	    "data": {
	        "user_id": "yujiang",
	        "display_name": "YuJiang",
	        "email": "",
	        "suspended": 0,
	        "max_buckets": 1000,
	        "auid": 0,
	        "subusers": [],
	        "keys": [
	            {
	                "user": "yujiang",
	                "access_key": "5863KD18AHSK9WBEDD0K",
	                "secret_key": "4x3U6zPkjKW8NzedkZ5KkfvtnNXJw18joIDx4LX4"
	            }
	        ],
	        "swift_keys": [],
	        "caps": [],
	        "op_mask": "read, write, delete",
	        "default_placement": "",
	        "placement_tags": [],
	        "bucket_quota": {
	            "enabled": false,
	            "max_size_kb": -1,
	            "max_objects": -1
	        },
	        "user_quota": {
	            "enabled": false,
	            "max_size_kb": -1,
	            "max_objects": -1
	        },
	        "temp_url_keys": [],
	        "attrs": [
	            {
	                "key": "user.rgw.idtag",
	                "val": ""
	            },
	            {
	                "key": "user.rgw.manifest",
	                "val": ""
	            }
	        ]
	    }
	}


	radosgw-admin metadata get bucket:123
	{
	    "key": "bucket:123",
	    "ver": {
	        "tag": "_pUvAdDsLKBLddMEIZd1Ggun",
	        "ver": 1
	    },
	    "mtime": "2016-08-15 02:25:21.678772Z",
	    "data": {
	        "bucket": {
	            "name": "123",
	            "pool": "default.rgw.buckets.data",
	            "data_extra_pool": "default.rgw.buckets.non-ec",
	            "index_pool": "default.rgw.buckets.index",
	            "marker": "3c585bf2-1983-48ee-83c8-a573007113ad.14106.1",
	            "bucket_id": "3c585bf2-1983-48ee-83c8-a573007113ad.14106.1"
	        },
	        "owner": "yujiang",
	        "creation_time": "0.000000",
	        "linked": "true",
	        "has_bucket_info": "false"
	    }
	}
