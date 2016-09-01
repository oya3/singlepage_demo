# gulp ���C���X�g�[������Ă��Ȃ��ꍇ
$ npm install -g gulp

# git ����{�v���W�F�N�g���擾�����ꍇ�A�ȉ��̃R�}���h�����{����K�v������
$ bower install
$ npm install
$ gulp
��node_modules/smoothie/smoothie.js �̊Ď��∳�k����肭���삵�Ă��Ȃ�����


�Q�l�T�C�g�F
* npm + gulp + bower �Ńr���h������
http://int128.hatenablog.com/entry/2014/07/02/004543
* package.json��npm���Ǘ�����
http://alice345.hatenablog.com/entry/2014/01/14/152316


# --------------------------------------------------------------------------------
# �ȉ��̃T�C�g�ɏ]���Ċ��\�z���Ă݂�
# http://blog.asial.co.jp/1370
# �x�[�X�f���T�C�g�Fhttp://www.wecloud.net.cn/onsenUI/demo/carousel/index.html
# �x�[�X�f���\�[�X�Fhttps://github.com/OnsenUI/OnsenUI/releases/tag/1.3.19
# --------------------------------------------------------------------------------

# �v���W�F�N�g�i��Ɓj�f�B���N�g���쐬����
$ mkdir onsenui_test


# onsenui �p�b�P�[�W���C���X�g�[�����邽�� bower ���C���X�g�[������
$ npm install -g bower

# onsenui ���C���X�g�[������
#  �J�����g�f�B���N�g���� bower_components �ɃC���X�g�[�������
$ bower install onsenui --save

# Gulp �𗘗p���Ď��s���ɕK�v�ȃt�@�C���Q��Z�߂�igrunt �Ɠ��l�̂��j
# �ȉ���qiita�L��������悤�ɂǂ��� gulp,grunt�͗��s���ĂȂ�����������B�B�B
# [�Ӗ�]����Gulp��Grunt������������R
#  http://qiita.com/chuck0523/items/dafdbd19c12efd40e2de
$ cd onsenui_test
$ npm init
# �₢���킹���ڂ��������邪author,license ���炢���ȉ��̂悤�ɂ���̓f�t�H���g�ł���
# �f�t�H���g�͂��̂܂܉������͂������s����΂������|�C�B
author : �����̖��O
license: MIT

# npm init �� package.json �����������B���̂ɕK�v�� gulp �p�b�P�[�W�Q���C���X�g�[������
$ npm install -g gulp # �O���[�o���ɂ��C���X�g�[��
$ npm install --save-dev gulp # ���[�J���ɂ��C���X�g�[��
$ npm install --save-dev gulp-changed # �������牺��Gulp�̃v���O�C���ł��B
$ npm install --save-dev gulp-concat
$ npm install --save-dev gulp-coffee
$ npm install --save-dev gulp-uglify
$ npm install --save-dev gulp-sourcemaps
$ npm install --save-dev gulp-webserver
$ npm install --save-dev del

# gulp�p�ݒ�t�@�C�����쐬����
$ emacs gulpfile.js
var gulp = require('gulp');
var coffee = require('gulp-coffee');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var webserver = require('gulp-webserver');
var sourcemaps = require('gulp-sourcemaps');
var del = require('del');
 
var paths = {
  scripts: ['app/js/**/*.coffee', '!app/external/**/*.coffee']
};
 
// Web�T�[�o�̋@�\�ł�
gulp.task('webserver', function() {
  gulp.src(&quot;./&quot;)
    .pipe(webserver({
      livereload: true,
    }));
});
 
// �X�N���v�g�̌����Ɣz�u���s���Ă��܂�
gulp.task('scripts', function() {
  return gulp.src([
      './bower_components/onsenui/build/js/angular/angular.min.js', // �����͍ŐV�̃p�X�ɕύX����K�v������
      './bower_components/onsenui/build/js/onsenui_all.min.js'      // �����͍ŐV�̃p�X�ɕύX����K�v������
  ])
    .pipe(concat('all.js'))
    .pipe(gulp.dest('./javascripts/'));
});
 
// �t�@�C���̕ύX���Ď����Ă��܂��i����͎g���Ă��܂���j
gulp.task('watch', function() {
  gulp.watch(paths.scripts, ['scripts']);
});
 
gulp.task('default', ['webserver', 'scripts', 'watch']);


# webserver, scripts, watch �S���𓮍삳����ɂ�
$ gulp

# webserver �������삳����ɂ�
$ gulp webserver

# scripts �������삳����ɂ�
$ gulp scripts




