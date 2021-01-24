- dog_n_cup.mp4: https://bjpublic-my.sharepoint.com/:v:/g/personal/bjpublic_bjpublic_co_kr/EYSXHq87jL9Gkj-QWArZs6EBr481ACJ7U7WM_r8VyOJdng?e=57pmHz
- oxford-flowers-17: http://www.robots.ox.ac.uk/~vgg/data/flowers/17/17flowers.tgz
  - 아래와 같이 class별로 directory 분할이 필요합니다.
    ```python
    import os
    import glob
    from shutil import copyfile
    from pathlib import Path

    img_list = sorted(glob.glob('17flowers/jpg/*.jpg'))
    print('There are', len(img_list), 'images.')

    class_num = 0
    target_base_path = './17flowers_div'

    for i, file_path in enumerate(img_list):
        if i % 80 == 0:
            if i != 0:
                class_num+=1
            dir_path = os.path.join(target_base_path, str(class_num).zfill(4))
            Path(dir_path).mkdir(parents=True, exist_ok=True)

        target_path = os.path.join(dir_path, file_path.split('/')[-1])
        copyfile(file_path, target_path)

    print(i+1, 'images divided into', class_num+1, 'classes completed.')
    ```
