import 'dart:async';
import 'dart:math' as math;

import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

void main() => runApp(const GhostStudyApp());

// ---------------------------------------------------------------------------
// Renkler ve ortak stiller
// ---------------------------------------------------------------------------
class AppColors {
  static const Color purple = Color(0xFF6C4DF6);
  static const Color purpleDark = Color(0xFF4B2FC9);
  static const Color purpleSoft = Color(0xFFEDE8FF);
  static const Color blue = Color(0xFF3B82F6);
  static const Color blueSoft = Color(0xFFE4F0FF);
  static const Color teal = Color(0xFF14B8A6);
  static const Color pink = Color(0xFFEF6C8B);
  static const Color bg = Color(0xFFF7F5FF);
  static const Color ink = Color(0xFF2A2350);
  static const Color muted = Color(0xFF7A7499);
}

const TextStyle kTitleStyle = TextStyle(
  fontSize: 17,
  fontWeight: FontWeight.w700,
  color: AppColors.ink,
);

const TextStyle kMutedStyle = TextStyle(
  fontSize: 13,
  color: AppColors.muted,
);

// ---------------------------------------------------------------------------
// Modeller
// ---------------------------------------------------------------------------
class Task {
  String title;
  String category;
  bool done;
  Task(this.title, this.category, {this.done = false});
}

class Note {
  String text;
  DateTime time;
  Note(this.text, this.time);
}

// ---------------------------------------------------------------------------
// Uygulama
// ---------------------------------------------------------------------------
class GhostStudyApp extends StatelessWidget {
  const GhostStudyApp({super.key});

  @override
  Widget build(BuildContext context) {
    final scheme = ColorScheme.fromSeed(
      seedColor: AppColors.purple,
      brightness: Brightness.light,
    ).copyWith(
      primary: AppColors.purple,
      secondary: AppColors.blue,
    );

    return MaterialApp(
      title: 'GhostStudy',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        useMaterial3: true,
        brightness: Brightness.light,
        colorScheme: scheme,
        scaffoldBackgroundColor: AppColors.bg,
        filledButtonTheme: FilledButtonThemeData(
          style: FilledButton.styleFrom(
            backgroundColor: AppColors.purple,
            foregroundColor: Colors.white,
            padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 14),
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(16),
            ),
            textStyle: const TextStyle(fontWeight: FontWeight.w700),
          ),
        ),
        textButtonTheme: TextButtonThemeData(
          style: TextButton.styleFrom(foregroundColor: AppColors.purple),
        ),
      ),
      home: const HomeShell(),
    );
  }
}

// ---------------------------------------------------------------------------
// Ana ekran
// ---------------------------------------------------------------------------
class HomeShell extends StatefulWidget {
  const HomeShell({super.key});

  @override
  State<HomeShell> createState() => _HomeShellState();
}

class _HomeShellState extends State<HomeShell> with TickerProviderStateMixin {
  final math.Random _rng = math.Random();

  late final AnimationController _floatCtrl;
  late final AnimationController _bounceCtrl;

  int _tab = 0;

  // Hayalet / konuşma balonu
  String _bubble = '';
  bool _bubbleVisible = false;
  Timer? _bubbleTimer;
  String _lastMsg = '';

  // Pomodoro
  int _mode = 0; // 0: 25/5, 1: 50/10, 2: özel
  int _focusMin = 25;
  int _breakMin = 5;
  int _customFocus = 40;
  int _customBreak = 8;
  bool _isFocus = true;
  bool _running = false;
  int _remaining = 25 * 60;
  int _sessions = 0;
  int _focusMinutesTotal = 0;
  Timer? _ticker;

  // Görevler
  final List<Task> _tasks = [
    Task('Lineer Cebir: 3. ünite tekrarı', 'Ders'),
    Task('Fizik laboratuvar raporu', 'Ödev'),
  ];
  final List<String> _categories = ['Ders', 'Ödev', 'Sınav', 'Proje'];
  String _taskCategory = 'Ders';
  final TextEditingController _taskCtrl = TextEditingController();

  // Notlar
  final List<Note> _notes = [];
  final TextEditingController _noteCtrl = TextEditingController();
  final TextEditingController _searchCtrl = TextEditingController();
  String _search = '';

  @override
  void initState() {
    super.initState();
    _floatCtrl = AnimationController(
      vsync: this,
      duration: const Duration(seconds: 4),
    )..repeat();
    _bounceCtrl = AnimationController(
      vsync: this,
      duration: const Duration(milliseconds: 600),
    );
    WidgetsBinding.instance.addPostFrameCallback((_) {
      if (mounted) _say(_timeGreeting(), seconds: 8);
    });
  }

  @override
  void dispose() {
    _ticker?.cancel();
    _bubbleTimer?.cancel();
    _floatCtrl.dispose();
    _bounceCtrl.dispose();
    _taskCtrl.dispose();
    _noteCtrl.dispose();
    _searchCtrl.dispose();
    super.dispose();
  }

  // -------------------------------------------------------------------------
  // Yardımcılar
  // -------------------------------------------------------------------------
  String _fmt(int s) {
    final m = (s ~/ 60).toString().padLeft(2, '0');
    final sec = (s % 60).toString().padLeft(2, '0');
    return '$m:$sec';
  }

  String _fmtDate(DateTime d) {
    String two(int n) => n.toString().padLeft(2, '0');
    return '${two(d.day)}.${two(d.month)}.${d.year}  ${two(d.hour)}:${two(d.minute)}';
  }

  void _snack(String message) {
    if (!mounted) return;
    final messenger = ScaffoldMessenger.of(context);
    messenger.hideCurrentSnackBar();
    messenger.showSnackBar(
      SnackBar(
        content: Text(message),
        behavior: SnackBarBehavior.floating,
        backgroundColor: AppColors.ink,
        duration: const Duration(seconds: 3),
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(14)),
      ),
    );
  }

  Color _catColor(String c) {
    switch (c) {
      case 'Ders':
        return AppColors.purple;
      case 'Ödev':
        return AppColors.blue;
      case 'Sınav':
        return AppColors.pink;
      default:
        return AppColors.teal;
    }
  }

  Widget _card({required Widget child, EdgeInsets? padding}) {
    return Container(
      width: double.infinity,
      padding: padding ?? const EdgeInsets.all(18),
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(24),
        boxShadow: [
          BoxShadow(
            color: AppColors.purple.withOpacity(0.08),
            blurRadius: 22,
            offset: const Offset(0, 8),
          ),
        ],
      ),
      child: child,
    );
  }

  InputDecoration _inputDec(String hint, {IconData? icon}) {
    return InputDecoration(
      hintText: hint,
      hintStyle: const TextStyle(color: AppColors.muted, fontSize: 14),
      prefixIcon: icon == null ? null : Icon(icon, color: AppColors.purple),
      filled: true,
      fillColor: AppColors.bg,
      contentPadding: const EdgeInsets.symmetric(horizontal: 16, vertical: 14),
      border: OutlineInputBorder(
        borderRadius: BorderRadius.circular(16),
        borderSide: BorderSide.none,
      ),
      focusedBorder: OutlineInputBorder(
        borderRadius: BorderRadius.circular(16),
        borderSide: const BorderSide(color: AppColors.purple, width: 1.5),
      ),
    );
  }

  // -------------------------------------------------------------------------
  // Hayalet mantığı
  // -------------------------------------------------------------------------
  String _timeGreeting() {
    final h = DateTime.now().hour;
    if (h < 5) {
      return 'Gece yarısı çalışması mı Ela? Ben yanındayım ama uykunu da ihmal etme 🌙';
    }
    if (h < 12) {
      return 'Günaydın Ela! ☀️ Bugün için enerjin tam, hadi başlayalım!';
    }
    if (h < 18) {
      return 'Merhaba Ela! 👻 Öğleden sonra odak zamanı, hazır mısın?';
    }
    return 'İyi akşamlar Ela! 🌆 Günün son turlarını birlikte bitirelim.';
  }

  String _nextMessage() {
    final pending = _tasks.where((t) => !t.done).length;
    final pool = <String>[
      'Selam Ela! Ben Ghost 👻 Seninle çalışmak çok eğlenceli!',
      'Ela, küçük adımlar büyük sınavları geçirir ✨',
      'Biraz su içmeye ne dersin Ela? 💧',
      'Ela, telefonu sessize al; sadece birkaç dakikalık odak yeter! 📵',
      'Harika gidiyorsun Ela, seninle gurur duyuyorum 💜',
      'Ders bitince kendine küçük bir ödül vermeyi unutma Ela 🍪',
      'Omuzlarını gevşet, derin bir nefes al Ela 🌬️',
      'Ela, dün yaptığından bir adım ilerisi bugünün hedefi 🚀',
    ];
    if (pending > 0) {
      pool.add('Ela, bekleyen $pending görevin var. En kolayından başla, ivme gelir! 🚀');
    } else {
      pool.add('Ela, görev listen tertemiz! Yeni bir hedef ekleyelim mi? 🎯');
    }
    if (_sessions > 0) {
      pool.add('Ela, bugün $_sessions odak turu bitirdin, toplam $_focusMinutesTotal dakika! 🔥');
    }
    if (_running) {
      pool.add(_isFocus
          ? 'Odaktasın Ela, kalan süre ${_fmt(_remaining)} ⏳'
          : 'Mola zamanı Ela, kalan süre ${_fmt(_remaining)} ☕');
    } else {
      pool.add('Ela, bir Pomodoro başlatalım mı? Süreyi sen seç! ⏱️');
    }
    if (_notes.isNotEmpty) {
      pool.add('Ela, ${_notes.length} notun var; sınavdan önce göz atmayı unutma 📝');
    }
    pool.remove(_lastMsg);
    return pool[_rng.nextInt(pool.length)];
  }

  void _say(String message, {int seconds = 7}) {
    _bubbleTimer?.cancel();
    setState(() {
      _bubble = message;
      _lastMsg = message;
      _bubbleVisible = true;
    });
    _bubbleTimer = Timer(Duration(seconds: seconds), () {
      if (mounted) setState(() => _bubbleVisible = false);
    });
  }

  void _heyGhost() {
    _bounceCtrl.forward(from: 0);
    HapticFeedback.lightImpact();
    _say(_nextMessage());
  }

  // -------------------------------------------------------------------------
  // Pomodoro mantığı
  // -------------------------------------------------------------------------
  void _applyMode(int m) {
    _ticker?.cancel();
    setState(() {
      _mode = m;
      if (m == 0) {
        _focusMin = 25;
        _breakMin = 5;
      } else if (m == 1) {
        _focusMin = 50;
        _breakMin = 10;
      } else {
        _focusMin = _customFocus;
        _breakMin = _customBreak;
      }
      _isFocus = true;
      _running = false;
      _remaining = _focusMin * 60;
    });
  }

  Future<bool> _customDialog() async {
    final fc = TextEditingController(text: '$_customFocus');
    final bc = TextEditingController(text: '$_customBreak');
    String? error;
    final result = await showDialog<bool>(
      context: context,
      builder: (ctx) => StatefulBuilder(
        builder: (ctx, setD) => AlertDialog(
          backgroundColor: Colors.white,
          shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(24)),
          title: const Text('Özel süre belirle'),
          content: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              TextField(
                controller: fc,
                keyboardType: TextInputType.number,
                inputFormatters: [FilteringTextInputFormatter.digitsOnly],
                decoration: _inputDec('Odak süresi (dakika)', icon: Icons.bolt_rounded),
              ),
              const SizedBox(height: 12),
              TextField(
                controller: bc,
                keyboardType: TextInputType.number,
                inputFormatters: [FilteringTextInputFormatter.digitsOnly],
                decoration: _inputDec('Mola süresi (dakika)', icon: Icons.coffee_rounded),
              ),
              if (error != null)
                Padding(
                  padding: const EdgeInsets.only(top: 10),
                  child: Text(
                    error!,
                    style: TextStyle(color: Colors.red.shade600, fontSize: 12),
                  ),
                ),
            ],
          ),
          actions: [
            TextButton(
              onPressed: () => Navigator.pop(ctx, false),
              child: const Text('Vazgeç'),
            ),
            FilledButton(
              onPressed: () {
                final f = int.tryParse(fc.text.trim());
                final b = int.tryParse(bc.text.trim());
                if (f == null || b == null || f < 1 || f > 180 || b < 1 || b > 60) {
                  setD(() => error = 'Odak 1-180, mola 1-60 dakika arasında olmalı.');
                  return;
                }
                _customFocus = f;
                _customBreak = b;
                Navigator.pop(ctx, true);
              },
              child: const Text('Uygula'),
            ),
          ],
        ),
      ),
    );
    return result ?? false;
  }

  Future<void> _pickMode(int m) async {
    if (m == 2) {
      final ok = await _customDialog();
      if (!ok) return;
    }
    _applyMode(m);
    if (m == 2) {
      _say('Özel süre hazır Ela: $_customFocus dk odak, $_customBreak dk mola 🎛️');
    } else {
      _say('${m == 0 ? "25/5" : "50/10"} modu seçildi Ela. Hazır olunca başlat! ⏱️');
    }
  }

  void _toggleTimer() {
    if (_running) {
      _ticker?.cancel();
      setState(() => _running = false);
      _say('Duraklattık Ela. Hazır olunca devam ederiz ⏸️');
    } else {
      setState(() => _running = true);
      _ticker = Timer.periodic(const Duration(seconds: 1), (_) => _tick());
      _say(_isFocus
          ? 'Başlıyoruz Ela! Şimdi sadece ders ve sen varsın 🎧'
          : 'Mola başladı Ela, biraz esne ve su iç ☕');
    }
  }

  void _tick() {
    if (!mounted) return;
    if (_remaining > 1) {
      setState(() => _remaining--);
    } else {
      _phaseDone();
    }
  }

  void _phaseDone({bool skipped = false}) {
    HapticFeedback.mediumImpact();
    SystemSound.play(SystemSoundType.alert);
    String msg;
    setState(() {
      if (_isFocus) {
        if (!skipped) {
          _sessions++;
          _focusMinutesTotal += _focusMin;
        }
        _isFocus = false;
        _remaining = _breakMin * 60;
      } else {
        _isFocus = true;
        _remaining = _focusMin * 60;
      }
    });
    if (!_isFocus) {
      msg = skipped
          ? 'Moladasın Ela, biraz nefes al ☕'
          : 'Harika iş Ela! 🎉 $_sessions. turu tamamladın, $_breakMin dakika mola hak ettin!';
    } else {
      msg = 'Mola bitti Ela! 💪 Yeni bir odak turuna hazır mısın?';
    }
    _say(msg, seconds: 9);
    _snack(msg);
  }

  void _skipPhase() => _phaseDone(skipped: true);

  void _resetTimer() {
    _ticker?.cancel();
    setState(() {
      _running = false;
      _isFocus = true;
      _remaining = _focusMin * 60;
    });
    _say('Sayaç sıfırlandı Ela. Temiz bir başlangıç! 🔄');
  }

  // -------------------------------------------------------------------------
  // Görev mantığı
  // -------------------------------------------------------------------------
  void _addTask() {
    final text = _taskCtrl.text.trim();
    if (text.isEmpty) {
      _say('Ela, önce görevin adını yazmalısın 😊');
      return;
    }
    setState(() {
      _tasks.insert(0, Task(text, _taskCategory));
      _taskCtrl.clear();
    });
    FocusScope.of(context).unfocus();
    _say('"$text" listene eklendi Ela! Sen yaparsın 💪');
  }

  void _toggleTask(Task t, bool value) {
    setState(() => t.done = value);
    if (value) {
      final allDone = _tasks.every((x) => x.done);
      _say(allDone
          ? 'Tüm görevler tamam Ela! 🎉 Bugün efsanesin!'
          : 'Aferin Ela! Bir görev daha bitti ✅');
    }
  }

  void _deleteTask(Task t) {
    setState(() => _tasks.remove(t));
    _say('Görev listeden kaldırıldı Ela 🗑️');
  }

  void _clearCompleted() {
    setState(() => _tasks.removeWhere((t) => t.done));
    _say('Tamamlananlar temizlendi Ela, tertemiz! ✨');
  }

  // -------------------------------------------------------------------------
  // Not mantığı
  // -------------------------------------------------------------------------
  void _addNote() {
    final text = _noteCtrl.text.trim();
    if (text.isEmpty) {
      _say('Ela, kaydetmek için önce bir şeyler yaz 📝');
      return;
    }
    setState(() {
      _notes.insert(0, Note(text, DateTime.now()));
      _noteCtrl.clear();
    });
    FocusScope.of(context).unfocus();
    _say('Notun güvende Ela 📌');
  }

  Future<void> _editNote(Note n) async {
    final ctrl = TextEditingController(text: n.text);
    final result = await showDialog<String>(
      context: context,
      builder: (ctx) => AlertDialog(
        backgroundColor: Colors.white,
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(24)),
        title: const Text('Notu düzenle'),
        content: TextField(
          controller: ctrl,
          minLines: 3,
          maxLines: 8,
          autofocus: true,
          decoration: _inputDec('Notunu yaz...'),
        ),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(ctx),
            child: const Text('Vazgeç'),
          ),
          FilledButton(
            onPressed: () => Navigator.pop(ctx, ctrl.text.trim()),
            child: const Text('Kaydet'),
          ),
        ],
      ),
    );
    if (result != null && result.isNotEmpty) {
      setState(() => n.text = result);
      _say('Not güncellendi Ela ✏️');
    }
  }

  void _deleteNote(Note n) {
    setState(() => _notes.remove(n));
    _say('Not silindi Ela 🗑️');
  }

  Future<void> _copyNote(Note n) async {
    await Clipboard.setData(ClipboardData(text: n.text));
    _snack('Not panoya kopyalandı');
  }

  List<Note> get _filteredNotes {
    if (_search.trim().isEmpty) return _notes;
    final q = _search.trim().toLowerCase();
    return _notes.where((n) => n.text.toLowerCase().contains(q)).toList();
  }

  // -------------------------------------------------------------------------
  // Üst alan: Hey Ghost butonu + hayalet + konuşma balonu
  // -------------------------------------------------------------------------
  Widget _buildGhost(double size) {
    return GestureDetector(
      onTap: _heyGhost,
      child: AnimatedBuilder(
        animation: Listenable.merge([_floatCtrl, _bounceCtrl]),
        builder: (context, _) {
          final t = _floatCtrl.value;
          final dy = math.sin(t * 2 * math.pi) * 5;
          double blink = 0;
          if (t > 0.9 && t < 0.97) {
            blink = math.sin((t - 0.9) / 0.07 * math.pi);
          }
          final b = _bounceCtrl.value;
          final scale = 1 + 0.18 * math.sin(b * math.pi);
          final rot = 0.2 * math.sin(b * math.pi * 2);
          final excited = _bounceCtrl.isAnimating;
          return Transform.translate(
            offset: Offset(0, dy),
            child: Transform.rotate(
              angle: rot,
              child: Transform.scale(
                scale: scale,
                child: SizedBox(
                  width: size,
                  height: size * 1.08,
                  child: CustomPaint(
                    painter: GhostPainter(blink: blink, excited: excited),
                  ),
                ),
              ),
            ),
          );
        },
      ),
    );
  }

  Widget _buildHeader() {
    final compact = MediaQuery.of(context).viewInsets.bottom > 0;
    return Container(
      decoration: BoxDecoration(
        gradient: const LinearGradient(
          begin: Alignment.topLeft,
          end: Alignment.bottomRight,
          colors: [Color(0xFFE9E1FF), Color(0xFFDCEBFF)],
        ),
        borderRadius: const BorderRadius.vertical(bottom: Radius.circular(32)),
        boxShadow: [
          BoxShadow(
            color: AppColors.purple.withOpacity(0.15),
            blurRadius: 24,
            offset: const Offset(0, 10),
          ),
        ],
      ),
      child: SafeArea(
        bottom: false,
        child: Padding(
          padding: const EdgeInsets.fromLTRB(20, 12, 20, 16),
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              Row(
                crossAxisAlignment: CrossAxisAlignment.center,
                children: [
                  Expanded(
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      mainAxisSize: MainAxisSize.min,
                      children: [
                        const Text(
                          'GhostStudy',
                          style: TextStyle(
                            fontSize: 13,
                            fontWeight: FontWeight.w800,
                            color: AppColors.purpleDark,
                            letterSpacing: 0.4,
                          ),
                        ),
                        const SizedBox(height: 4),
                        const Text(
                          'Merhaba Ela! 👋',
                          style: TextStyle(
                            fontSize: 26,
                            fontWeight: FontWeight.w800,
                            color: AppColors.ink,
                          ),
                        ),
                        if (!compact) ...[
                          const SizedBox(height: 2),
                          const Text('Bugün neleri başaracağız?', style: kMutedStyle),
                        ],
                        const SizedBox(height: 10),
                        ElevatedButton.icon(
                          onPressed: _heyGhost,
                          icon: const Icon(Icons.waving_hand_rounded, size: 18),
                          label: const Text('Hey Ghost'),
                          style: ElevatedButton.styleFrom(
                            backgroundColor: AppColors.purple,
                            foregroundColor: Colors.white,
                            elevation: 6,
                            shadowColor: AppColors.purple.withOpacity(0.5),
                            shape: const StadiumBorder(),
                            padding: const EdgeInsets.symmetric(
                              horizontal: 20,
                              vertical: 12,
                            ),
                            textStyle: const TextStyle(
                              fontSize: 15,
                              fontWeight: FontWeight.w800,
                            ),
                          ),
                        ),
                      ],
                    ),
                  ),
                  const SizedBox(width: 8),
                  _buildGhost(compact ? 64 : 96),
                ],
              ),
              if (!compact)
                AnimatedSize(
                  duration: const Duration(milliseconds: 250),
                  alignment: Alignment.topCenter,
                  child: _bubbleVisible
                      ? Column(
                          children: [
                            Align(
                              alignment: Alignment.centerRight,
                              child: Padding(
                                padding: const EdgeInsets.only(right: 39),
                                child: CustomPaint(
                                  size: const Size(18, 9),
                                  painter: _TailPainter(),
                                ),
                              ),
                            ),
                            Container(
                              width: double.infinity,
                              padding: const EdgeInsets.symmetric(
                                horizontal: 16,
                                vertical: 12,
                              ),
                              decoration: BoxDecoration(
                                color: Colors.white,
                                borderRadius: BorderRadius.circular(18),
                                boxShadow: [
                                  BoxShadow(
                                    color: AppColors.purple.withOpacity(0.12),
                                    blurRadius: 14,
                                    offset: const Offset(0, 5),
                                  ),
                                ],
                              ),
                              child: AnimatedSwitcher(
                                duration: const Duration(milliseconds: 250),
                                child: Text(
                                  _bubble,
                                  key: ValueKey(_bubble),
                                  style: const TextStyle(
                                    fontSize: 14,
                                    height: 1.35,
                                    color: AppColors.ink,
                                    fontWeight: FontWeight.w600,
                                  ),
                                ),
                              ),
                            ),
                          ],
                        )
                      : const SizedBox(width: double.infinity, height: 0),
                ),
            ],
          ),
        ),
      ),
    );
  }

  // -------------------------------------------------------------------------
  // Sekme 1: Pomodoro
  // -------------------------------------------------------------------------
  Widget _modeChip(int index, String label) {
    final selected = _mode == index;
    return ChoiceChip(
      label: Text(label),
      selected: selected,
      showCheckmark: false,
      selectedColor: AppColors.purple,
      backgroundColor: AppColors.purpleSoft,
      side: BorderSide.none,
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(14)),
      labelStyle: TextStyle(
        fontWeight: FontWeight.w700,
        color: selected ? Colors.white : AppColors.purpleDark,
      ),
      onSelected: (_) => _pickMode(index),
    );
  }

  Widget _stat(IconData icon, String value, String label, Color color) {
    return Expanded(
      child: Container(
        padding: const EdgeInsets.symmetric(vertical: 14, horizontal: 8),
        decoration: BoxDecoration(
          color: Colors.white,
          borderRadius: BorderRadius.circular(20),
          boxShadow: [
            BoxShadow(
              color: AppColors.purple.withOpacity(0.07),
              blurRadius: 16,
              offset: const Offset(0, 6),
            ),
          ],
        ),
        child: Column(
          children: [
            Icon(icon, color: color, size: 22),
            const SizedBox(height: 6),
            Text(
              value,
              style: const TextStyle(
                fontSize: 20,
                fontWeight: FontWeight.w800,
                color: AppColors.ink,
              ),
            ),
            const SizedBox(height: 2),
            Text(
              label,
              textAlign: TextAlign.center,
              style: const TextStyle(fontSize: 11, color: AppColors.muted),
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildTimerTab() {
    final total = (_isFocus ? _focusMin : _breakMin) * 60;
    final progress = (1 - _remaining / total).clamp(0.0, 1.0);
    final c1 = _isFocus ? AppColors.purple : AppColors.blue;
    final c2 = _isFocus ? AppColors.blue : AppColors.teal;
    final ringSize = math.max(170.0, math.min(260.0, MediaQuery.of(context).size.width - 96));
    final pending = _tasks.where((t) => !t.done).length;

    return ListView(
      padding: const EdgeInsets.fromLTRB(16, 18, 16, 24),
      children: [
        _card(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Row(
                children: [
                  const Text('Pomodoro', style: kTitleStyle),
                  const Spacer(),
                  Container(
                    padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 5),
                    decoration: BoxDecoration(
                      color: (_isFocus ? AppColors.purple : AppColors.teal).withOpacity(0.12),
                      borderRadius: BorderRadius.circular(20),
                    ),
                    child: Text(
                      _isFocus ? 'Odak' : 'Mola',
                      style: TextStyle(
                        fontWeight: FontWeight.w800,
                        fontSize: 12,
                        color: _isFocus ? AppColors.purpleDark : AppColors.teal,
                      ),
                    ),
                  ),
                ],
              ),
              const SizedBox(height: 12),
              Wrap(
                spacing: 8,
                runSpacing: 8,
                children: [
                  _modeChip(0, '25 / 5'),
                  _modeChip(1, '50 / 10'),
                  _modeChip(2, 'Özel ($_customFocus/$_customBreak)'),
                ],
              ),
              const SizedBox(height: 22),
              Center(
                child: SizedBox(
                  width: ringSize,
                  height: ringSize,
                  child: Stack(
                    alignment: Alignment.center,
                    children: [
                      CustomPaint(
                        size: Size(ringSize, ringSize),
                        painter: RingPainter(progress: progress, c1: c1, c2: c2),
                      ),
                      Column(
                        mainAxisSize: MainAxisSize.min,
                        children: [
                          Text(
                            _fmt(_remaining),
                            style: const TextStyle(
                              fontSize: 52,
                              fontWeight: FontWeight.w800,
                              color: AppColors.ink,
                            ),
                          ),
                          const SizedBox(height: 4),
                          Text(
                            _isFocus ? 'Odaklan Ela 💜' : 'Mola zamanı ☕',
                            style: kMutedStyle,
                          ),
                        ],
                      ),
                    ],
                  ),
                ),
              ),
              const SizedBox(height: 22),
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  IconButton.filledTonal(
                    onPressed: _resetTimer,
                    tooltip: 'Sıfırla',
                    icon: const Icon(Icons.replay_rounded),
                  ),
                  const SizedBox(width: 16),
                  FilledButton.icon(
                    onPressed: _toggleTimer,
                    icon: Icon(_running ? Icons.pause_rounded : Icons.play_arrow_rounded),
                    label: Text(_running ? 'Duraklat' : 'Başlat'),
                  ),
                  const SizedBox(width: 16),
                  IconButton.filledTonal(
                    onPressed: _skipPhase,
                    tooltip: 'Sonraki aşamaya geç',
                    icon: const Icon(Icons.skip_next_rounded),
                  ),
                ],
              ),
            ],
          ),
        ),
        const SizedBox(height: 14),
        Row(
          children: [
            _stat(Icons.local_fire_department_rounded, '$_sessions', 'Tamamlanan tur', AppColors.pink),
            const SizedBox(width: 10),
            _stat(Icons.schedule_rounded, '$_focusMinutesTotal', 'Odak dakikası', AppColors.blue),
            const SizedBox(width: 10),
            _stat(Icons.checklist_rounded, '$pending', 'Bekleyen görev', AppColors.purple),
          ],
        ),
      ],
    );
  }

  // -------------------------------------------------------------------------
  // Sekme 2: Görevler
  // -------------------------------------------------------------------------
  Widget _taskTile(Task t) {
    final c = _catColor(t.category);
    return Container(
      margin: const EdgeInsets.only(bottom: 10),
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(18),
        border: Border.all(color: c.withOpacity(0.18)),
        boxShadow: [
          BoxShadow(
            color: AppColors.purple.withOpacity(0.05),
            blurRadius: 12,
            offset: const Offset(0, 4),
          ),
        ],
      ),
      child: InkWell(
        borderRadius: BorderRadius.circular(18),
        onTap: () => _toggleTask(t, !t.done),
        child: Padding(
          padding: const EdgeInsets.fromLTRB(6, 8, 4, 8),
          child: Row(
            children: [
              Checkbox(
                value: t.done,
                activeColor: AppColors.purple,
                shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(6)),
                onChanged: (v) => _toggleTask(t, v ?? false),
              ),
              Expanded(
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(
                      t.title,
                      style: TextStyle(
                        fontSize: 15,
                        fontWeight: FontWeight.w600,
                        color: t.done ? AppColors.muted : AppColors.ink,
                        decoration: t.done ? TextDecoration.lineThrough : TextDecoration.none,
                      ),
                    ),
                    const SizedBox(height: 6),
                    Container(
                      padding: const EdgeInsets.symmetric(horizontal: 10, vertical: 3),
                      decoration: BoxDecoration(
                        color: c.withOpacity(0.12),
                        borderRadius: BorderRadius.circular(10),
                      ),
                      child: Text(
                        t.category,
                        style: TextStyle(
                          fontSize: 11,
                          fontWeight: FontWeight.w800,
                          color: c,
                        ),
                      ),
                    ),
                  ],
                ),
              ),
              IconButton(
                tooltip: 'Sil',
                onPressed: () => _deleteTask(t),
                icon: const Icon(Icons.delete_outline_rounded, color: AppColors.muted),
              ),
            ],
          ),
        ),
      ),
    );
  }

  Widget _buildTasksTab() {
    final done = _tasks.where((t) => t.done).length;
    final total = _tasks.length;
    final pendingList = _tasks.where((t) => !t.done).toList();
    final doneList = _tasks.where((t) => t.done).toList();

    return ListView(
      padding: const EdgeInsets.fromLTRB(16, 18, 16, 24),
      children: [
        _card(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              const Text('Yeni görev / ders', style: kTitleStyle),
              const SizedBox(height: 12),
              TextField(
                controller: _taskCtrl,
                textInputAction: TextInputAction.done,
                onSubmitted: (_) => _addTask(),
                decoration: _inputDec(
                  'Örn. Mikroekonomi 4. bölüm tekrarı',
                  icon: Icons.edit_note_rounded,
                ),
              ),
              const SizedBox(height: 12),
              Wrap(
                spacing: 8,
                runSpacing: 8,
                children: _categories.map((c) {
                  final selected = _taskCategory == c;
                  final col = _catColor(c);
                  return ChoiceChip(
                    label: Text(c),
                    selected: selected,
                    showCheckmark: false,
                    selectedColor: col,
                    backgroundColor: col.withOpacity(0.10),
                    side: BorderSide.none,
                    shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(14)),
                    labelStyle: TextStyle(
                      fontWeight: FontWeight.w700,
                      color: selected ? Colors.white : col,
                    ),
                    onSelected: (_) => setState(() => _taskCategory = c),
                  );
                }).toList(),
              ),
              const SizedBox(height: 14),
              SizedBox(
                width: double.infinity,
                child: FilledButton.icon(
                  onPressed: _addTask,
                  icon: const Icon(Icons.add_rounded),
                  label: const Text('Listeye ekle'),
                ),
              ),
            ],
          ),
        ),
        const SizedBox(height: 14),
        _card(
          padding: const EdgeInsets.all(16),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              Row(
                children: [
                  const Text('İlerleme', style: kTitleStyle),
                  const Spacer(),
                  Text(
                    '$done / $total tamamlandı',
                    style: const TextStyle(
                      fontWeight: FontWeight.w700,
                      color: AppColors.purpleDark,
                      fontSize: 13,
                    ),
                  ),
                ],
              ),
              const SizedBox(height: 10),
              ClipRRect(
                borderRadius: BorderRadius.circular(10),
                child: LinearProgressIndicator(
                  value: total == 0 ? 0 : done / total,
                  minHeight: 10,
                  backgroundColor: AppColors.purpleSoft,
                  valueColor: const AlwaysStoppedAnimation<Color>(AppColors.purple),
                ),
              ),
            ],
          ),
        ),
        const SizedBox(height: 16),
        if (_tasks.isEmpty)
          _card(
            child: const Column(
              children: [
                Text('👻', style: TextStyle(fontSize: 40)),
                SizedBox(height: 8),
                Text('Listen boş görünüyor', style: kTitleStyle),
                SizedBox(height: 4),
                Text(
                  'İlk dersini veya görevini yukarıdan ekle.',
                  style: kMutedStyle,
                  textAlign: TextAlign.center,
                ),
              ],
            ),
          ),
        ...pendingList.map(_taskTile),
        if (doneList.isNotEmpty) ...[
          const SizedBox(height: 6),
          Row(
            children: [
              const Padding(
                padding: EdgeInsets.only(left: 4),
                child: Text('Tamamlananlar', style: kTitleStyle),
              ),
              const Spacer(),
              TextButton.icon(
                onPressed: _clearCompleted,
                icon: const Icon(Icons.cleaning_services_rounded, size: 18),
                label: const Text('Temizle'),
              ),
            ],
          ),
          const SizedBox(height: 6),
          ...doneList.map(_taskTile),
        ],
      ],
    );
  }

  // -------------------------------------------------------------------------
  // Sekme 3: Hızlı notlar
  // -------------------------------------------------------------------------
  Widget _noteCard(Note n) {
    return Container(
      width: double.infinity,
      margin: const EdgeInsets.only(bottom: 10),
      padding: const EdgeInsets.fromLTRB(16, 10, 8, 14),
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(18),
        border: Border.all(color: AppColors.blue.withOpacity(0.15)),
        boxShadow: [
          BoxShadow(
            color: AppColors.purple.withOpacity(0.05),
            blurRadius: 12,
            offset: const Offset(0, 4),
          ),
        ],
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Row(
            children: [
              const Icon(Icons.sticky_note_2_rounded, size: 16, color: AppColors.blue),
              const SizedBox(width: 6),
              Expanded(
                child: Text(
                  _fmtDate(n.time),
                  style: const TextStyle(fontSize: 12, color: AppColors.muted),
                ),
              ),
              IconButton(
                tooltip: 'Kopyala',
                visualDensity: VisualDensity.compact,
                onPressed: () => _copyNote(n),
                icon: const Icon(Icons.copy_rounded, size: 18, color: AppColors.muted),
              ),
              IconButton(
                tooltip: 'Düzenle',
                visualDensity: VisualDensity.compact,
                onPressed: () => _editNote(n),
                icon: const Icon(Icons.edit_rounded, size: 18, color: AppColors.muted),
              ),
              IconButton(
                tooltip: 'Sil',
                visualDensity: VisualDensity.compact,
                onPressed: () => _deleteNote(n),
                icon: const Icon(Icons.delete_outline_rounded, size: 20, color: AppColors.muted),
              ),
            ],
          ),
          const SizedBox(height: 4),
          Padding(
            padding: const EdgeInsets.only(right: 8),
            child: SelectableText(
              n.text,
              style: const TextStyle(fontSize: 15, height: 1.4, color: AppColors.ink),
            ),
          ),
        ],
      ),
    );
  }

  Widget _prefixChip(String label, String prefix) {
    return ActionChip(
      label: Text(label),
      backgroundColor: AppColors.blueSoft,
      side: BorderSide.none,
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(14)),
      labelStyle: const TextStyle(
        color: AppColors.blue,
        fontWeight: FontWeight.w700,
        fontSize: 12,
      ),
      onPressed: () {
        final cur = _noteCtrl.text;
        final next = cur.isEmpty ? prefix : '$cur\n$prefix';
        _noteCtrl.value = TextEditingValue(
          text: next,
          selection: TextSelection.collapsed(offset: next.length),
        );
      },
    );
  }

  Widget _buildNotesTab() {
    final list = _filteredNotes;
    return ListView(
      padding: const EdgeInsets.fromLTRB(16, 18, 16, 24),
      children: [
        _card(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              const Text('Hızlı not', style: kTitleStyle),
              const SizedBox(height: 12),
              TextField(
                controller: _noteCtrl,
                minLines: 3,
                maxLines: 6,
                keyboardType: TextInputType.multiline,
                decoration: _inputDec('Aklındakini hemen yaz, sonra unutma...'),
              ),
              const SizedBox(height: 10),
              Wrap(
                spacing: 8,
                runSpacing: 4,
                children: [
                  _prefixChip('📌 Önemli', '📌 Önemli: '),
                  _prefixChip('📖 Kaynak', '📖 Kaynak: '),
                  _prefixChip('💡 Fikir', '💡 Fikir: '),
                ],
              ),
              const SizedBox(height: 12),
              SizedBox(
                width: double.infinity,
                child: FilledButton.icon(
                  onPressed: _addNote,
                  icon: const Icon(Icons.save_rounded),
                  label: const Text('Notu kaydet'),
                ),
              ),
            ],
          ),
        ),
        const SizedBox(height: 14),
        TextField(
          controller: _searchCtrl,
          onChanged: (v) => setState(() => _search = v),
          decoration: _inputDec('Notlarda ara', icon: Icons.search_rounded).copyWith(
            fillColor: Colors.white,
            suffixIcon: _search.isEmpty
                ? null
                : IconButton(
                    icon: const Icon(Icons.close_rounded),
                    onPressed: () {
                      _searchCtrl.clear();
                      setState(() => _search = '');
                    },
                  ),
          ),
        ),
        const SizedBox(height: 14),
        if (_notes.isEmpty)
          _card(
            child: const Column(
              children: [
                Text('📝', style: TextStyle(fontSize: 40)),
                SizedBox(height: 8),
                Text('Henüz not yok', style: kTitleStyle),
                SizedBox(height: 4),
                Text(
                  'Derste duyduğun bir formülü veya bir fikri hemen kaydet.',
                  style: kMutedStyle,
                  textAlign: TextAlign.center,
                ),
              ],
            ),
          )
        else if (list.isEmpty)
          _card(
            child: const Center(
              child: Text('Aramanla eşleşen not bulunamadı.', style: kMutedStyle),
            ),
          )
        else
          ...list.map(_noteCard),
      ],
    );
  }

  // -------------------------------------------------------------------------
  // Build
  // -------------------------------------------------------------------------
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          _buildHeader(),
          Expanded(
            child: IndexedStack(
              index: _tab,
              children: [
                _buildTimerTab(),
                _buildTasksTab(),
                _buildNotesTab(),
              ],
            ),
          ),
        ],
      ),
      bottomNavigationBar: NavigationBar(
        selectedIndex: _tab,
        backgroundColor: Colors.white,
        surfaceTintColor: Colors.transparent,
        indicatorColor: AppColors.purpleSoft,
        onDestinationSelected: (i) {
          FocusScope.of(context).unfocus();
          setState(() => _tab = i);
        },
        destinations: const [
          NavigationDestination(
            icon: Icon(Icons.timer_outlined),
            selectedIcon: Icon(Icons.timer_rounded, color: AppColors.purple),
            label: 'Odak',
          ),
          NavigationDestination(
            icon: Icon(Icons.checklist_rounded),
            selectedIcon: Icon(Icons.checklist_rounded, color: AppColors.purple),
            label: 'Görevler',
          ),
          NavigationDestination(
            icon: Icon(Icons.sticky_note_2_outlined),
            selectedIcon: Icon(Icons.sticky_note_2_rounded, color: AppColors.purple),
            label: 'Notlar',
          ),
        ],
      ),
    );
  }
}

// ---------------------------------------------------------------------------
// Çizimler: Hayalet, konuşma balonu kuyruğu, zamanlayıcı halkası
// ---------------------------------------------------------------------------
class GhostPainter extends CustomPainter {
  final double blink; // 0 = açık, 1 = kapalı
  final bool excited;

  const GhostPainter({required this.blink, required this.excited});

  @override
  void paint(Canvas canvas, Size size) {
    final w = size.width;
    final h = size.height;

    // Gövde
    final body = Path()
      ..moveTo(0.1 * w, 0.88 * h)
      ..lineTo(0.1 * w, 0.42 * h)
      ..arcToPoint(
        Offset(0.9 * w, 0.42 * h),
        radius: Radius.circular(0.4 * w),
        clockwise: true,
      )
      ..lineTo(0.9 * w, 0.88 * h);
    final seg = 0.8 * w / 4;
    double x = 0.9 * w;
    for (int i = 0; i < 4; i++) {
      final cy = i.isEven ? h : 0.74 * h;
      body.quadraticBezierTo(x - seg / 2, cy, x - seg, 0.88 * h);
      x -= seg;
    }
    body.close();

    canvas.drawShadow(body, AppColors.purple.withOpacity(0.55), 8, false);

    final fill = Paint()
      ..shader = const LinearGradient(
        begin: Alignment.topCenter,
        end: Alignment.bottomCenter,
        colors: [Colors.white, Color(0xFFE6DEFF)],
      ).createShader(Rect.fromLTWH(0, 0, w, h));
    final outline = Paint()
      ..style = PaintingStyle.stroke
      ..strokeWidth = 1.5
      ..color = AppColors.purple.withOpacity(0.28);

    // Kollar
    void arm(double cx, double cy, double angle) {
      canvas.save();
      canvas.translate(cx, cy);
      canvas.rotate(angle);
      final r = Rect.fromCenter(center: Offset.zero, width: 0.2 * w, height: 0.1 * w);
      canvas.drawOval(r, fill);
      canvas.drawOval(r, outline);
      canvas.restore();
    }

    final armAngle = excited ? 1.0 : 0.6;
    arm(0.06 * w, 0.6 * h, -armAngle);
    arm(0.94 * w, 0.6 * h, armAngle);

    canvas.drawPath(body, fill);
    canvas.drawPath(body, outline);

    // Gözler
    final eyePaint = Paint()..color = AppColors.ink;
    final eyeY = 0.44 * h;
    final ry = (0.075 * h) * (1 - blink) + 0.006 * h;
    for (final cx in [0.36 * w, 0.64 * w]) {
      canvas.drawOval(
        Rect.fromCenter(center: Offset(cx, eyeY), width: 0.12 * w, height: ry * 2),
        eyePaint,
      );
      if (blink < 0.5) {
        canvas.drawCircle(
          Offset(cx + 0.015 * w, eyeY - 0.02 * h),
          0.014 * w,
          Paint()..color = Colors.white,
        );
      }
    }

    // Yanaklar
    final cheek = Paint()..color = const Color(0xFFFFB6D1).withOpacity(0.75);
    canvas.drawOval(
      Rect.fromCenter(center: Offset(0.25 * w, 0.56 * h), width: 0.12 * w, height: 0.07 * w),
      cheek,
    );
    canvas.drawOval(
      Rect.fromCenter(center: Offset(0.75 * w, 0.56 * h), width: 0.12 * w, height: 0.07 * w),
      cheek,
    );

    // Ağız
    if (excited) {
      final mouthRect = Rect.fromCenter(
        center: Offset(0.5 * w, 0.54 * h),
        width: 0.18 * w,
        height: 0.13 * h,
      );
      canvas.drawArc(mouthRect, 0, math.pi, true, Paint()..color = AppColors.ink);
      canvas.drawOval(
        Rect.fromCenter(center: Offset(0.5 * w, 0.585 * h), width: 0.08 * w, height: 0.035 * h),
        Paint()..color = const Color(0xFFFF8FB1),
      );
    } else {
      final smile = Paint()
        ..style = PaintingStyle.stroke
        ..strokeCap = StrokeCap.round
        ..strokeWidth = 0.025 * w
        ..color = AppColors.ink;
      canvas.drawArc(
        Rect.fromCenter(center: Offset(0.5 * w, 0.52 * h), width: 0.14 * w, height: 0.07 * h),
        0.2,
        math.pi - 0.4,
        false,
        smile,
      );
    }
  }

  @override
  bool shouldRepaint(covariant GhostPainter old) =>
      old.blink != blink || old.excited != excited;
}

class _TailPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final p = Path()
      ..moveTo(0, size.height)
      ..lineTo(size.width / 2, 0)
      ..lineTo(size.width, size.height)
      ..close();
    canvas.drawPath(p, Paint()..color = Colors.white);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}

class RingPainter extends CustomPainter {
  final double progress;
  final Color c1;
  final Color c2;

  const RingPainter({required this.progress, required this.c1, required this.c2});

  @override
  void paint(Canvas canvas, Size size) {
    const stroke = 16.0;
    final center = size.center(Offset.zero);
    final radius = (size.shortestSide - stroke) / 2;
    final rect = Rect.fromCircle(center: center, radius: radius);

    final track = Paint()
      ..style = PaintingStyle.stroke
      ..strokeWidth = stroke
      ..color = AppColors.purpleSoft;
    canvas.drawCircle(center, radius, track);

    if (progress > 0) {
      final arc = Paint()
        ..style = PaintingStyle.stroke
        ..strokeWidth = stroke
        ..strokeCap = StrokeCap.round
        ..shader = SweepGradient(
          startAngle: 0,
          endAngle: 2 * math.pi,
          colors: [c1, c2, c1],
          transform: const GradientRotation(-math.pi / 2),
        ).createShader(rect);
      canvas.drawArc(rect, -math.pi / 2, 2 * math.pi * progress, false, arc);
    }
  }

  @override
  bool shouldRepaint(covariant RingPainter old) =>
      old.progress != progress || old.c1 != c1 || old.c2 != c2;
}
